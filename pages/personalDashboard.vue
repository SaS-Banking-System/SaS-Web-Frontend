<template>
    <div class="wrapper">
        <Navbar />
        <h1>Personal dashboard</h1>
        <div class="pageContent">
            <h2>Your balance is €</h2>
            <div class="transactionList">
                <TransactionList />
            </div>
        </div>
    </div>
</template>

<style scoped>
.wrapper {
    width: 100vw;
    height: 100vh;
    background-color: white;
}

.pageContent {
    margin-left: 26rem;
    display: flex;
    justify-content: center;
}

h1 {
    margin-left: 9.4rem;
    font-size: 3rem;
    font-weight: 400;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

h2 {
    font-size: 2rem;
    font-weight: 400;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.transactionList {
    
}
</style>