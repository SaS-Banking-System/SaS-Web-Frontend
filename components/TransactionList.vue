<script setup>

</script>

<template>
    <div class="wrapper">
        <h1>Transaktionen</h1>
        <ol class="transactions">
            <li>
                <p>10<img src="dollar.svg"> bekommen am 03.01.2024</p>
                <p>20<img src="dollar.svg"> gesendet am 02.01.2024</p>
                <p>140<img src="dollar.svg"> bekommen am 02.01.2024</p>
                <p>140<img src="dollar.svg"> bekommen am 01.01.2024</p>
                <p>50<img src="dollar.svg"> gesendet am 01.01.2024</p>
                <p>100<img src="dollar.svg"> bekommen am 01.01.2024</p>
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
    border-bottom: 2px solid ;
    color: black;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

h1 {
    border-radius: 10px;
    background-color: var(--dashboardHeaderColours);
    padding: 4px;
    color: black;
    font-size: 2rem;
    font-weight: 400;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}
</style>