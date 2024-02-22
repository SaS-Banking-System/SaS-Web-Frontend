<script setup lang="ts">
const props = defineProps(["transactions", "uuid"]);
</script>

<template>
  <div class="wrapper">
    <h1>Transaktionen</h1>
    <ol
      v-for="transaction in props.transactions.reverse()"
      class="transactions"
    >
      <li>
        <p
          v-if="String(transaction.sender) === String(props.uuid)"
          class="transaction-send"
        >
          {{ Number(transaction.amount) + Number(transaction.tax) }}
          <img src="/dollar.svg" /> gesendet am {{ transaction.createdAt }}
        </p>
        <p v-else class="transaction-received">
          {{ transaction.amount }} <img src="/dollar.svg" /> bekommen am
          {{ transaction.createdAt }}
        </p>
      </li>
    </ol>
  </div>
</template>

<style scoped>
.wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
}

img {
  margin-inline-start: 0.2rem;
  width: 0.75rem;
  color: black;
}

.transactions {
  margin: 0;
  margin-top: 1.5vh;
  padding: 0;
  list-style-type: none;
  background: rgba(255, 255, 255, 0.959);
  filter: drop-shadow(0px 0px 5px rgba(53, 85, 92, 0.9));
  border-radius: 5px;
}

p {
  margin-inline: 1rem;
  border-bottom: 2px solid;
  color: black;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
}

h1 {
  border-radius: 10px;
  background-color: rgb(198, 229, 247);
  padding: 4px;
  color: black;
  font-size: 2rem;
  font-weight: 400;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
}

.transaction-send {
  background-color: rgba(255, 0, 0, 0.286);
  border-top-right-radius: 10px;
  border-top-left-radius: 10px;
}
.transaction-received {
  background-color: rgba(113, 246, 80, 0.447);
  border-top-right-radius: 10px;
  border-top-left-radius: 10px;
}
</style>
