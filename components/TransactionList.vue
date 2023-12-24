<template>
    <div class="wrapper">
        <h1>Transactions</h1>
        <ol class="transactions">
            <li>You received 200€ from blabla</li>
            <li>You received 200€ from blabla</li>
            <li>You received 200€ from blabla</li>
            <li>You received 200€ from blabla</li>
            <li>You received 200€ from blabla</li>
            <li>You received 200€ from blabla</li>
            <li>You received 200€ from blabla</li>
        </ol>
    </div>
</template>

<style scoped>
.wrapper {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
}

.transactions {
    margin: 0;
    padding: 0;
    margin-left: 7.9vw;
    list-style-type: none;
    background: rgba(245, 245, 245, 0.829);
    border-radius: 10px;
}

h1 {
    margin-left: 7.8vw;
    font-size: 2rem;
    font-weight: 400;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

</style>