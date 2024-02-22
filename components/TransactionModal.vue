<script setup lang="ts">
const props = defineProps(['show', 'sender'])

import { QrcodeStream } from 'vue-qrcode-reader'

let sanitizedReceiverUUID = ref<string>('')
let receiverUUID = ref<string>('')
let sanitizedScannerUUID = ref<string>('')
sanitizedScannerUUID.value = new Array(Math.floor(props.sender.length / 2)).fill('*').join('') + props.sender.slice(Math.ceil(props.sender.length / 2), props.sender.length);

let scanFinished = ref<boolean>(false)
let modalHeight = ref<string>('65vh')
let transactionSuccess =  ref<boolean>(false)
let amount = ref<number>(0)
let notNumberError = ref<boolean>(false)

function onDetect(detected: string) {
    const code = (detected[0] as any).rawValue

	sanitizedReceiverUUID.value = new Array(Math.floor(code.length / 2)).fill('*').join('') +
										code.slice(Math.ceil(code.length / 2), code.length);

    receiverUUID.value = code;
    scanFinished.value = true;
    modalHeight.value = '40vh';
}

async function handleTransaction() {
    if (!String(amount.value).match(/^[0-9]+$/)) {
        return;
    }

	const transactionRequest = await useFetch('http://localhost:3001/transaction/new', {
		method: 'post',
		body: {
			sender: String(props.sender),
			receiver: receiverUUID,
			amount: Number(amount.value)
		},
	})

	if (!transactionRequest || transactionRequest.status.value === 'error') { 
		console.log('something went wrong')
  	    return
    }

	transactionSuccess.value = true;
}
</script>

<template>
    <Transition name="modal">
        <div v-if="props.show" class="wrapper">
            <div :style="{height: modalHeight}" class="modal-container">
                <div class="transaction-info-header">
                    <p >Neue Transaktion</p>
                </div>
                <div class="transaction-info-body">
                    <p>Absender: {{ sanitizedScannerUUID }}</p>
                    <p>Empfänger: {{ sanitizedReceiverUUID }}</p>
                </div>
                <div v-if="!scanFinished" class="reader-wrapper">
                    <qrcode-stream @detect="onDetect"></qrcode-stream>
                </div>
                <form type="text" class="form">
                    <input id="amountInput" type="number" v-model="amount" placeholder="Betrag eingeben...">
                </form>
                <p class="errorcode" v-if="notNumberError">Bitte eine Zahl eingeben.</p>
                <div class="transaction-info-footer">
                    <button class="cancel" @click="$emit('close')">Abbrechen</button>
                    <button class="sendTransaction" @click="handleTransaction" :disabled="transactionSuccess">Absenden</button>
                </div>
            </div>  
        </div>
    </Transition>
</template>

<style scoped>
p {
    font-weight: 500;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.errorcode {
    color: rgb(240, 56, 56);
    font-size: 1.2rem;
}

.form {
    width: 21%;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
}
.form > input {
    width: 100%;
    border: 1px solid rgb(180, 180, 180);
    border-radius: 5px;
    padding-inline-start: 5px;
    margin-left: 8px;
    font-size: 1.2rem;
    outline: none;
}

.form > input:focus {
    outline: 2px solid rgba(125, 169, 252, 0.747);
    filter: drop-shadow(0px 0px 3px rgb(125, 169, 252, 0.747));
}

.transaction-info-header {
    display: flex;
    justify-content: center;
}
.transaction-info-header > p {
    font-size: 2rem;
    font-weight: 700;
    text-decoration: underline;
    color: rgb(48, 165, 83);
}
.transaction-info-body > p {
    font-size: 1.2rem;
}
.transaction-info-footer {
    margin-top: 2vh
}
.reader-wrapper {
	display: flex;
	flex-direction: center;
	justify-content: center;
	margin-left: 25%;
	width: 50%;
}

.wrapper {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    transition: opacity 0.3s ease;
}

.modal-container {
    width: 40vw;
    height: 65vh;
    margin: auto;
    padding: 10px 30px;

    border-radius: 10px;
    background-color: white;
    box-shadow: 0 0px 10px rgba(0, 0, 0, 0.8);
    transition: all 0.3s ease;
}

.receiverForm {
    margin-bottom: 20px;
}

.cancel {
    all: unset;
    font-size: 1.2rem;
    font-weight: 500;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    border-radius: 10px;
    padding: 10px;
    border: 2px solid rgb(146, 146, 146);
    color: rgb(61, 61, 61);
    float: right;
}

.sendTransaction {
    all: unset;
    font-size: 1.2rem;
    font-weight: 500;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    border-radius: 10px;
    padding: 12px;
    background-color: rgb(64, 197, 119);
    color: white;
}

.cancel:hover {
    background-color: rgb(241, 241, 241);
    color: rgb(41, 41, 41);
    cursor: pointer;
}
.sendTransaction:hover {
    background-color: rgb(52, 156, 95);
    cursor: pointer;
}

.modal-enter-from {
    opacity: 0;
}

.modal-leave-to {
    opacity: 0;
}

.modal-enter-from .modal-container,
.modal-leave-to .modal-container {
    -webkit-transform: scale(1.1);
    transform: scale(1.1);
}
</style>