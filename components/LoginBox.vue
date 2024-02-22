<script setup>
import { QrcodeStream } from "vue-qrcode-reader";

const scannedUUID = ref("");
let wrongUUID = ref(false);
let scanFinished = ref(false);
let loginRequest = ref(false);
let modalHeight = ref("80vh");

function rescan() {
  location.reload();
}

function onDetect(detected) {
  scannedUUID.value = detected[0].rawValue;

  scanFinished.value = true;
  modalHeight.value = "60vh";
}

async function login() {
  const uuidCookie = useCookie("uuid");
  uuidCookie.value = scannedUUID.value;

  loginRequest.value = true;

  const userRequest = await useFetch(
    `http://localhost:3001/account/exist/${uuidCookie.value}`,
  );

  if (!userRequest || userRequest.status.value === "error") {
    wrongUUID.value = true;
    return;
  }

  loginRequest.value = false;

  navigateTo("/personalDashboard");
}
</script>

<template>
  <div class="login">
    <div class="mar">
      <div :style="{ height: modalHeight }" class="loginbox">
        <h1>Login</h1>
        <br />
        <form type="text" class="form">
          <input
            :value="scannedUUID"
            id="formInput"
            type="text"
            placeholder="Scan dein QR-Code..."
            readonly
          />
        </form>

        <div v-if="!scanFinished" class="reader-wrapper">
          <qrcode-stream @detect="onDetect"></qrcode-stream>
        </div>

        <p v-if="wrongUUID" class="wrong-uuid">UUID nicht gefunden</p>

        <button :disabled="loginRequest" @click="login" class="dashboardLink">
          <p class="loginButton">Anmelden</p>
        </button>

        <div v-if="scanFinished">
          <button @click="rescan" class="rescanButton">Nochmal Scannen</button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.reader-wrapper {
  width: 80%;
  margin-bottom: 5vh;
}
.loginbox {
  width: 37%;
  transition: height 0.3s;
  margin: auto;
  margin-top: 13vh;
  border-radius: 10px;
  background-color: white;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  filter: drop-shadow(0px 0px 7px rgb(201, 201, 201));
}

@media only screen and (max-width: 1444px) {
  .loginbox {
    width: 100%;
  }
}

.mar {
  margin-inline: 12vw;
}
h1 {
  font-size: 2.6rem;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  margin-bottom: 7vh;
}
.form {
  width: 80%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
.form > input {
  width: 100%;
  border: 1px solid rgb(180, 180, 180);
  border-radius: 5px;
  padding-inline-start: 10px;
  margin-bottom: 5vh;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  font-size: 1.5rem;
  outline: none;
}

.form > input:focus {
  outline: 2px solid rgba(125, 169, 252, 0.747);
  filter: drop-shadow(0px 0px 3px rgb(125, 169, 252, 0.747));
}

.form > input:focus ~ .qrCodeScanner {
  display: block;
}

.loginButton {
  all: unset;
  width: 80%;
  background-color: rgb(47, 116, 219);
  transition: background-color 0.2s;
  color: white;
  border-radius: 5px;
  margin-bottom: 12vh;
  padding-top: 12px;
  padding-bottom: 12px;
}

.rescanButton {
  all: unset;
  background-color: rgb(47, 116, 219);
  transition: background-color 0.2s;
  color: white;
  border-radius: 5px;

  margin-bottom: 12vh;
  padding: 12px;

  font-weight: 500;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  font-size: 1.5rem;
}

.dashboardLink {
  all: unset;
  width: 100%;
  font-weight: 500;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  font-size: 1.5rem;
  text-align: center;
  display: flex;
  justify-content: center;
}

.loginButton:hover {
  background-color: rgb(41, 86, 153);
  cursor: pointer;
}

.rescanButton:hover {
  background-color: rgb(41, 86, 153);
  cursor: pointer;
}

.qrCodeScanner {
  display: none;
  margin-top: -3vh;
  margin-bottom: 3vh;
}
.wrong-uuid {
  color: red;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  font-size: 1.7rem;
}
</style>
