<script setup lang="ts">
import { QrcodeStream } from "vue-qrcode-reader";

const ccodeCookie = useCookie("ccode");

if (!ccodeCookie.value) await navigateTo("/checkout-login");

const ccode = ccodeCookie.value;
const companyRequest = await useFetch(
  `http://localhost:3001/company/info/${ccode}`,
);

if (!companyRequest || companyRequest.status.value === "error") {
  navigateTo("/checkout-login");
  useCookie("ccode").value = null;
}

let companyName: string = (companyRequest.data.value as any).name;

interface Product {
  value: number;
  productIndex: number;
}

let products = ref<Product[]>([]);
let index: number = 0;
let total = ref<number>(0);
let priceInput = ref<string>("");
let priceInputElement = ref();

function computeTotal() {
  let runningTotal = 0;

  products.value.map(({ value }) => {
    runningTotal += value;
  });

  total.value = runningTotal;
}

function addProduct() {
  if (!String(priceInput.value).match(/^[0-9]+$/)) {
    priceInput.value = "";
    return;
  }

  products.value.push({ value: Number(priceInput.value), productIndex: index });

  index++;

  priceInput.value = "";

  computeTotal();
}

function removeProduct(targetIndex: number) {
  const id = products.value.findIndex(
    (product) => product.productIndex === targetIndex,
  );

  if (id === -1) return;

  products.value.splice(id, 1);

  computeTotal();
}

function logout() {
  ccodeCookie.value = null;

  navigateTo("/");
}

// Modal
let modalOpen = ref<boolean>(false);
let sanitizedUUID = ref<string>("");
let uuid = ref<string>("");
let isScanned = ref<boolean>(false);
let transactionSuccess = ref<boolean>(false);
let transactionError = ref<boolean>(false);
let transactionLock = ref<boolean>(false);
let buttonWrapperMargin = ref<string>("22rem");

function handleModalClose() {
  modalOpen.value = false;
}

function handleModalOpen() {
  modalOpen.value = true;
}

function onDetect(detected: string) {
  const code = (detected[0] as any).rawValue;

  sanitizedUUID.value =
    new Array(Math.floor(code.length / 2)).fill("*").join("") +
    code.slice(Math.ceil(code.length / 2), code.length);

  uuid.value = code;
  isScanned.value = true;
}

function handleRescan() {
  isScanned.value = false;
  uuid.value = "";
  sanitizedUUID.value = "";
}

async function handleTransaction() {
  
  if(transactionLock.value) return;

  transactionLock.value = true;

  const transactionRequest = await useFetch(
    "http://localhost:3001/transaction/company/new",
    {
      method: "post",
      body: {
        sender: uuid.value,
        code: String(ccode),
        amount: Number(total.value),
      },
    },
  );

  transactionLock.value = false;

  if (!transactionRequest || transactionRequest.status.value === "error") {
    transactionError.value = true;
    buttonWrapperMargin.value = "17.6rem";
    return;
  }

  buttonWrapperMargin.value = "17.8rem";
  transactionSuccess.value = true;
  transactionError.value = false;
}

function newTransaction() {
  location.reload();
}
</script>

<template>
  <h1 class="company-name">{{ companyName }}</h1>
  <div class="checkout-wrapper">
    <div class="product-list">
      <div v-for="{ value, productIndex } in products" class="product">
        <p class="product-price">
          Preis: <strong>{{ value }}</strong> Rosen
        </p>
        <button
          @click="removeProduct(productIndex)"
          class="product-remove-button"
        >
          <div class="product-remove-button-svg">
            <PlusSvg color="red" :rotation="45" />
          </div>

          <p class="product-remove-button-text">Produkt entfernen</p>
        </button>
      </div>
    </div>

    <div class="utility-wrapper">
      <div class="utility-buttons">
        <button @click="addProduct" class="product-button">
          <div class="product-button-content">
            <PlusSvg color="white" />
            <p class="product-button-text">Preis hinzufügen</p>
          </div>
        </button>
        <input
          placeholder="Preis eingeben..."
          class="price-input"
          type="number"
          v-model="priceInput"
          ref="priceInputElement"
        />
      </div>
      <div class="checkout-utility-wrapper">
        <h1 class="total-text">
          INSGESAMT: <span class="total-text-value">{{ total }} Rosen </span>
        </h1>
        <button class="checkout-button" @click="handleModalOpen">
          <div class="checkout-button-content">
            <ShoppingCartSvg />
            <p class="checkout-button-text">Checkout</p>
          </div>
        </button>
      </div>
    </div>
    <button @click="logout" class="logout-button">Ausloggen</button>
  </div>

  <!-- Modal -->
  <Transition name="modal-transition">
    <div v-if="modalOpen" class="wrapper">
      <div class="modal">
        <button @click="handleModalClose" class="close-button">
          <PlusSvg color="black" :rotation="45" />
        </button>
        <h1 class="company-name-modal">{{ companyName }}</h1>
        <div class="transaction-info-wrapper">
          <p>
            Betrag: <span>{{ total }}</span>
          </p>
          <p>
            Empfänger: <span>{{ companyName }}</span>
          </p>
          <p>
            Von: <span>{{ sanitizedUUID }}</span>
          </p>
        </div>
        <div class="transaction-error-wrapper" v-if="transactionError">
          <p class="transaction-error-text">
            Es ist ein Fehler aufgetreten! Falls es noch einmal Probleme gibt,
            rufen sie einen Administrator.
          </p>
        </div>
        <div v-if="isScanned" class="modal-button-wrapper" :style="{ marginTop: buttonWrapperMargin }">
          <button :disabled="transactionSuccess" @click="handleRescan" class="modal-button-rescan">
            QR-Code erneut scannen
          </button>
          <button :disabled="transactionSuccess" @click="handleTransaction">
            Transaktion ausführen
          </button>
        </div>
        <div v-if="transactionSuccess">
          <p class="transaction-success-message">Transaktion erfolgreich!</p>
          <button class="button-new-transaction" @click="newTransaction">Neue Transaktion</button>
        </div>
        <div v-if="!isScanned" class="reader-wrapper">
          <qrcode-stream @detect="onDetect"></qrcode-stream>
        </div>
      </div>
    </div>
  </Transition>
</template>

<style scoped lang="scss">
:global(body) {
  height: 100%;
  background-color: white;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
}
.company-name {
  height: 5vh;
  text-align: center;
  font-size: 1.6rem;
  font-weight: bold;
  margin: 1rem 0;
}
.checkout-wrapper {
  height: 85vh;
  display: block;
}
.utility-wrapper {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  margin: 1rem;
}
.total-text {
  margin-block: auto;
  font-size: 1.7rem;
  display: flex;
  flex-direction: row;
  align-items: center;
}
.total-text-value {
  font-weight: bold;
  margin-inline: 0.6rem;
  margin-block: auto;
  border-bottom: solid 3px black;
}
.utility-buttons {
  display: flex;
  align-self: flex-start;
}
.price-input {
  all: unset;
  background-color: white;
  border: 1px solid rgb(180, 180, 180);
  display: flex;
  flex-direction: column;
  border-radius: 7px;
  margin-inline: 1rem;
  padding: 7px;
  font-size: 1.2rem;
}
.price-input:focus {
  outline: 2px solid rgba(125, 169, 252, 0.747);
  filter: drop-shadow(0px 0px 3px rgb(125, 169, 252, 0.747));
}
.checkout-utility-wrapper {
  display: flex;
}
.product-list {
  display: block;
  height: 60dvh;
  overflow: auto;
  background-color: rgb(243, 249, 253);
  border: 1px solid rgb(0, 0, 0);
}
.product {
  display: flex;
  border-radius: 10px;
  border: 1px solid gray;
  background-color: white;
  margin: 1rem 0.3rem;
  padding: 0.5rem 0.6rem;
}
.product-remove-button {
  font-size: 1.1rem;
  border: 4px solid rgb(224, 2, 2);
  background-color: white;
  display: flex;
  flex-direction: row;
}
.product-remove-button-text {
  color: rgb(224, 2, 2);
}
.product-remove-button:hover {
  background-color: #f0d8d8;
  transition: all 0.2s;
}
.product-price {
  margin-block: auto;
  font-size: 1.3rem;
}
strong {
  font-weight: bold;
}
.product > button {
  margin-left: 1rem;
}
.product-button {
  all: unset;
  background-color: #13c770;
  border-radius: 7px;
  font-weight: 500;
  cursor: pointer;
}
.product-button:hover {
  background-color: #0b9b55;
}
.product-button-content {
  display: flex;
  flex-direction: row;
  align-items: center;
  padding: 7px;
}
.product-button-text {
  font-size: 1.2rem;
  padding-inline: 5px;
  color: white;
}
.checkout-button {
  all: unset;
  background-color: #13c770;
  border-radius: 7px;
  font-weight: 500;
  cursor: pointer;
  margin-left: 1rem;
  padding: 0.3rem;
}
.checkout-button:hover {
  background-color: #0b9b55;
}
.checkout-button-content {
  display: flex;
  flex-direction: row;
  vertical-align: center;
  padding: 7px;
}
.checkout-button-text {
  font-size: 1.2rem;
  font-weight: bold;
  display: flex;
  flex-direction: column;
  padding-inline: 5px;
  color: white;
}
.logout-button {
  all: unset;
  cursor: pointer;
  color: rgb(224, 2, 2);
  font-weight: bold;
  border-radius: 10px;
  position: absolute;
  bottom: 2rem;
  right: 1rem;
  font-size: 1.3rem;
  padding: 0.7rem;
  border: 3px solid rgb(224, 2, 2);
  transition: all 0.2s;
}
.logout-button:hover {
  background-color: #ca0c0c;
  border: 3px solid #ca0c0c;
  color: white;
  transition: all 0.2s;
}

$clr-login-button: rgb(64, 197, 119);
.wrapper {
  position: fixed;
  display: block;
  height: 100vh;
  width: 100vw;
  top: 0%;
  left: 0%;
  backdrop-filter: brightness(60%);
  transition: opacity 0.3s ease;
}
.modal {
  display: block;
  position: fixed;
  height: 80%;
  width: 70%;
  z-index: 9999;
  background-color: white;
  top: 10%;
  left: 15%;
  border-radius: 10px;
  overflow: hidden;
  transition: all 0.3s ease;
}
.company-name-modal {
  display: flex;
  flex-direction: row;
  justify-content: center;
  font-size: 3rem;
  font-weight: 700;
  text-decoration: underline;
  color: rgb(48, 165, 83);
  margin-top: 1rem;
}
.transaction-info-wrapper {
  margin: 0rem 0rem 1rem 2rem;
}
.transaction-info-wrapper > p {
  font-size: 2rem;
  margin-top: 0.3rem;
}
.transaction-info-wrapper > p > span {
  font-weight: bold;
}
.close-button {
  all: unset;
  position: absolute;
  width: 3rem;
  height: 3rem;
  top: 0;
  right: 0;
  background-color: white;
  margin: 1rem 1rem 0 0;
  cursor: pointer;
}
.close-button:hover,
.close-button:focus {
  background-color: rgb(240, 240, 240);
  outline: 2px solid black;
  border-radius: 50%;
}
.reader-wrapper {
  display: flex;
  flex-direction: center;
  justify-content: center;
  margin-top: 2rem;
  margin-left: 25%;
  width: 50%;
}
#reader {
  width: 50%;
  aspect-ratio: 4 / 2;
}
button {
  all: unset;
  margin-left: 2rem;
  font-weight: 500;
  font-size: 1.4rem;
  color: white;
  background-color: $clr-login-button;
  padding: 12px;
  border-radius: 10px;
  cursor: pointer;
}
.success-transaction {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
}
button:hover {
  background-color: rgb(52, 156, 95);
}
button:disabled {
  display: none;
}
.modal-button-rescan {
  margin-right: 2rem;
  float: right;
}

.failed-transaction {
  text-align: center;
  font-size: 1.2rem;
  font-weight: bold;
  color: red;
}
.transaction-success-message {
  margin-left: 2rem;
  font-size: 1.8rem;
  font-weight: bold;
  color: rgb(52, 156, 95);
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
}
.product-remove-button-svg {
  height: 100%;
  display: flex;
}
.transaction-error-text {
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  color: rgb(221, 0, 0);
  font-size: 1.8rem;
  font-weight: bold;
  text-align: center;
}

.modal-transition-enter-from {
  opacity: 0;
}

.modal-transition-leave-to {
  opacity: 0;
}

.modal-transition-enter-from .modal,
.modal-transition-leave-to .modal {
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}
</style>
