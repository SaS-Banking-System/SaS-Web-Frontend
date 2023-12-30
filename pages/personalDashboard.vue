<script setup>
const uuid = 1234
const request = await useFetch(`http://212.227.150.82:3000/account/info/${uuid}`, {
    mode:
        "no-cors"
})
</script>

<template>
    <div class="wrapper">
        <Navbar />
        <div class="header">
            <h1>Personal dashboard</h1>
            <div class="pageContent">
                <h2>Your balance is {{ request.data.value.account.balance }}€</h2>
                <div class="transactionList">
                    <TransactionList :transactions="request.data.value.transactions" :uuid="uuid"/>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
.wrapper {
    background-color: rgb(10,10,10);
}

.header {
    display: flex;
    flex-direction: column;
}

.transactionList {
    width: 100%;
    margin-left: 7.9vw;
}

.pageContent {
    height: 93vh;
    margin-left: 6.5rem;
    display: flex;
}

h1 {
    color: white;
    margin-left: 9.4rem;
    font-size: 3rem;
    font-weight: 400;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

h2 {
    padding-inline: 3rem;
    color: white;
    font-size: 2rem;
    font-weight: 400;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}
</style>