<script setup>
const props = defineProps(['show', 'sender'])

import { QrcodeStream } from 'vue-qrcode-reader'

const scannedUUID = ref('')
let scanFinished = ref(false);

function rescan() {
    location.reload()
}

function onDetect(detected) {
    scannedUUID.value = detected[0].rawValue

    scanFinished.value = true;
}

</script>

<template>
    <div v-if="props.show" class="wrapper">
        <div class="modal-container">
            <p>Neue Transaktion</p>
            <p>Absender: {{ sender }}</p>
            <p>Empfänger: </p>
            <form type="text" class="receiverForm">
                <input :value="scannedUUID" id="receiverInput" type="text" placeholder="QR-Code des Empfängers scannen...">
            </form>
            <form type="text" class="amountForm">
                <input id="amountInput" type="text" placeholder="Betrag eingeben...">
            </form>
            <button class="cancel" @click="$emit('close')">Abbrechen</button>
        </div>  
    </div>
</template>

<style scoped>
.wrapper {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
}

.modal-container {
  width: 40vw;
  height: 60vh;
  margin: auto;
  padding: 20px 30px;

  border-radius: 2px;
  background-color: white;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
}

.receiverForm {
    margin-bottom: 20px;
}

.cancel {
    margin-top: 20px;
}
</style>