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
        <h1>Personal dashboard</h1>
        <div class="pageContent">
            <h2>Your balance is {{ request.data.value.account.balance }}€</h2>
            <div class="transactionList">
                <TransactionList :transactions="request.data.value.transactions" :uuid="uuid"/>
            </div>
        </div>
    </div>
</template>

<style scoped>
.wrapper {
    width: 100vw;
    height: 100vh;
    background-color: rgb(10,10,10);
}

.transactionList {
    width: 100%;
}

.pageContent {
    width: 100vw;
    margin-left: 26rem;
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
    flex-grow: 1;
    padding-inline: 3rem;
    color: white;
    font-size: 2rem;
    font-weight: 400;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}
</style>