<script setup>
  const uuidCookie = useCookie('uuid')

  if (!uuidCookie.value) await navigateTo('/login')

  const uuid = uuidCookie.value
  const userRequest = await useFetch(`http://localhost:3001/account/info/${uuid}`)

  if (!userRequest || userRequest.status.value === 'error') navigateTo('/login')

  const user = userRequest.data.value

  import TransactionModal from '~/components/TransactionModal.vue'
  import { ref } from 'vue'

  const showModal = ref(false)   
</script>

<template>
    <div class="wrapper">
        <Navbar />
        <div class="header">
            <h1>Persönliches Dashboard</h1>
            <div class="pageContent">
                <div class="balanceWrapper">
                    <h2>Dein Guthaben beträgt: </h2>
                    <p class="balance">{{ user.account.balance }}<img src="/dollar.svg" /></p>
                </div>
                <div class="transactionList">
                    <TransactionList :transactions="user.transactions" :uuid="uuid" />
                </div>
                <div>
                    <button class="buttontransaction">Neue Transaktion</button>
                    <div class="modalWrapper">
                        <TransactionModal :show="showModal" :sender="uuid" @close="showModal = false"></TransactionModal>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
.balanceWrapper {
    display: flex;
    flex-direction: column;
    align-items: center;
}

img {
    margin-left: 0.5rem;
    width: 2rem;
    color: black;
}

.balance {
    margin-left: 2.5vw;
    margin-top: -2vh;
    border-bottom: 4px dashed black;
    background-color: rgb(255, 255, 253);
    font-size: 3.5rem;
    font-weight: 400;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.header {
    display: flex;
    flex-direction: column;
    background-color: white;
    background-image: url("/dashboardbg2.svg");
    background-repeat: no-repeat;
    background-size: cover;
}

.transactionList {
    width: 100%;
    margin-top: 0.6vh;
    margin-left: 2vw;
}

.buttontransaction {
    margin-top: 12.2vh;
    margin-right: 47vw;
    white-space: nowrap;

    padding: 12px;
    border-radius: 12px;

    color: white;
    background-color: rgb(68, 216, 142);
    filter: drop-shadow(0px 0px 4px rgba(126, 126, 126, 0.8));

    font-weight: 500;
    font-size: 1.2rem;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.buttontransaction:hover {
    cursor: pointer;
}

.pageContent {
    height: 93vh;
    margin-left: 6.5rem;
    display: flex;
}

h1 {
    color: black;
    margin-left: 9.4rem;
    font-size: 3rem;
    text-decoration: underline;
    font-weight: 400;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

h2 {
    margin-left: 3vw;
    padding: 4px;
    color: black;
    border-radius: 10px;
    background-color: var(--dashboardHeaderColours);
    white-space: nowrap;
    font-size: 2rem;
    font-weight: 400;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}
</style>
