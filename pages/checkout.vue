<script setup lang="ts">
const ccodeCookie = useCookie('ccode')

if (!ccodeCookie.value) await navigateTo('/checkout-login')

const ccode = ccodeCookie.value
const companyRequest = await useFetch(`http://localhost:3001/company/info/${ccode}`)

if (!companyRequest || companyRequest.status.value === 'error') {
  navigateTo('/checkout-login')
  useCookie('ccode').value = null
} 

let companyName: string = (companyRequest.data.value as any).name

interface Product {
  value: number,
  productIndex: number,
}

let products = ref<Product[]>([])
let index: number = 0;
let total = ref<number>();
let priceInput = ref<string>();
let priceInputElement = ref();

function computeTotal() {
  let runningTotal = 0;

  products.value.map(({value}) => {
    runningTotal += value
  }) 

  total.value = runningTotal
}

function addProduct() {
  if (!String(priceInput.value).match(/^[0-9]+$/)) {
    priceInput.value = ''
    return;
  }

  products.value.push({ value: Number(priceInput.value), productIndex: index})

  index++;

  computeTotal()
}

function removeProduct(targetIndex: number) {
  const id = products.value.findIndex((product) => product.productIndex === targetIndex);

  if (id === -1) return;

  products.value.splice(id, 1);

  computeTotal()
}

function logout() {
  ccodeCookie.value = null

  navigateTo('/')
}
</script>

<template>
<h1 class="company-name">{{ companyName }}</h1>

<div class="checkout-wrapper">
	<div class="product-list">
			<div v-for="{value, productIndex} in products" class="product">
				<p class="product-price">Preis: <strong>{{ value }}</strong> Rosen</p>
				<button @click="removeProduct(productIndex)" class="product-remove-button" 
					><PlusSvg color="red" :rotation="45" /> Produkt entfernen</button
				>
			</div>
	</div>

	<div class="utility-wrapper">
		<div class="utility-buttons">
			<button @click="addProduct" class="product-button" 
				><div class="product-button-content">
					<PlusSvg />
					<p class="product-button-text">Preis Hinzufügen</p>
				</div></button
			>
			<input
				placeholder="Preis eingeben"
				class="price-input"
				type="number"
        v-model="priceInput"
        ref="priceInputElement"
			/>
		</div>
		<div class="checkout-utility-wrapper">
			<h1 class="total-text">
				INSGESAMT: <span class="total-text-value">{{ total }} Rosen</span>
			</h1>
			<button class="checkout-button" on:click={handleOpenCheckout}>
				<div class="checkout-button-content">
					  <ShoppingCartSvg />
					<p class="checkout-button-text">Checkout</p>
				</div>
			</button>
		</div>
	</div>
	<button @click="logout" class="logout-button" >Ausloggen</button>
</div>
</template>

<style scoped>
	:global(body) {
		height: 100%;
	}
	.company-name {
		height: 5vh;
		text-align: center;
		font-size: 1.5rem;
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
		font-size: 1.5rem;
		display: flex;
		flex-direction: row;
		align-items: center;
	}
	.total-text-value {
		font-weight: bold;
		margin-inline: 0.6rem;
		margin-block: auto;
	}
	.utility-buttons {
		display: flex;
		align-self: flex-start;
	}
	.price-input {
		all: unset;
		border: 1px solid gray;
		display: flex;
		flex-direction: column;
		border-radius: 7px;
		margin-inline: 1rem;
		padding: 7px;
		font-size: 1.2rem;
	}
	.price-input:focus {
		outline: 2px solid gray;
	}
	.checkout-utility-wrapper {
		display: flex;
	}
	.product-list {
		display: block;
		height: 60dvh;
		overflow: auto;
		border: 1px solid green;
	}
	.product {
		display: flex;
		border-radius: 10px;
		border: 1px solid gray;
		margin: 1rem 0.3rem;
		padding: 0.5rem 0.6rem;
	}
	.product-remove-button {
		font-size: 1.1rem;
		display: flex;
		flex-direction: row;
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
		background-color: #0ddd79;
		border-radius: 7px;
		cursor: pointer;
	}
	.product-button:hover {
		background-color: #0bc46b;
	}
	.product-button-content {
		display: flex;
		flex-direction: row;
		vertical-align: center;
		height: 100%;
		padding: 7px;
	}
	.product-button-text {
		font-size: 1.2rem;
		display: flex;
		flex-direction: column;
		padding-inline: 5px;
		color: white;
	}
	.checkout-button {
		all: unset;
		background-color: #0ddd79;
		border-radius: 7px;
		cursor: pointer;
		margin-left: 1rem;
		padding: 0.5rem;
	}
	.checkout-button:hover {
		background-color: #0bc46b;
	}
	.checkout-button-content {
		display: flex;
		flex-direction: row;
		vertical-align: center;
		height: 100%;
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
		color: white;
		border-radius: 10px;
		position: absolute;
		bottom: 2rem;
		right: 1rem;
		font-size: 1.3rem;
		padding: 0.7rem;
		background-color: red;
	}
	.logout-button:hover {
		background-color: #cc0000;
	}
</style>