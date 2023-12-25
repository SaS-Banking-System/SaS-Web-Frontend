<template>
    <div class="login">
        <div class="loginbox">
            <h1>Anmelden</h1><br>
            <form type="text" class="qrscanner">
                <input type="text" placeholder="Scan QR code...">
            </form>
            <button class="loginButton">
                <NuxtLink to="/personalDashboard">Login</NuxtLink>
            </button>
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
    flex-direction: column;
    justify-content: center;
    align-items: center;
    font-size: 1rem;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    filter: drop-shadow(0px 0px 7px rgb(201, 201, 201));
}
h1 {
    margin-bottom: 2vw;
}
.qrscanner > input {
    width: 22vw;
    height: 6vh;
    border: 1px solid rgb(180, 180, 180);
    border-radius: 5px;
    padding-inline-start: 10px;
    margin-bottom: 3vw;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    font-size: 1rem;
    outline: none;
}

.qrscanner > input:focus {
    outline: 2px solid rgba(125, 169, 252, 0.747);
    filter: drop-shadow(0px 0px 3px rgb(125, 169, 252, 0.747));
}

.loginButton {
    all: unset;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    font-size: 1.2rem;
    background-color: rgb(47, 116, 219);
    color: white;
    width: 100%;
    border-radius: 5px;
}

.loginButton > a {
    all: unset;
}

</style>