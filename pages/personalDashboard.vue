<template>
    <div class="wrapper">
        <Navbar />
        <h1>Personal dashboard</h1>
        <h2>Your balance is €</h2>
        <TransactionList />
    </div>
</template>

<style scoped>
.wrapper {
    width: 100vw;
    height: 100vh;
    background-color: white;
}

h1 {
    margin-left: 7.8vw;
    font-size: 3rem;
    font-weight: 400;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

h2 {
    margin-left: 7.8vw;
    font-size: 2rem;
    font-weight: 400;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}
</style>