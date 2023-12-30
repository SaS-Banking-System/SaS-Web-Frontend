<script setup>
const props = defineProps(['transactions', 'uuid'])
</script>

<template>
    <div class="wrapper">
        <h1>Transactions</h1>
        <ol class="transactions">
            <li v-for="transaction in props.transactions">
                <p v-if="String(props.uuid) === transaction.sender">You sent {{ transaction.amount }}€ with a {{ transaction.tax }}% tax on {{ transaction.createdAt }}</p>
                <p v-else>You received {{ transaction.amount }}€ with a {{ transaction.tax }}% tax on {{ Date(transaction.createdAt) }}</p>
            </li>
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
    list-style-type: none;
    background: rgba(112, 114, 122, 0.829);
    border-radius: 5px;
}

p {
    margin-inline: 1rem;
    color: white;
}

h1 {
    color: white;
    font-size: 2rem;
    font-weight: 400;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

</style>