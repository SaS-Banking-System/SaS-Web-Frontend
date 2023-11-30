<template>
    <div class="login">
        <div class="loginbox">
            <h1>Anmelden</h1><br>
            <form type="text" class="qrscanner">
                <input type="text">
            </form>
        </div>
    </div>
</template>

<style scoped>
.loginbox {
    width: 28vw;
    height: 60vh;
    margin: auto;
    margin-top: 20vh;
    border-radius: 10px;
    background-color: white;
    display: flex;
    justify-content: center;
    font-size: 1rem;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    filter: drop-shadow(0px 0px 7px rgb(201, 201, 201));
}

.qrscanner {
    margin-block: auto;
}
</style>