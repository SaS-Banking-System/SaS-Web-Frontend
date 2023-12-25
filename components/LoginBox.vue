<template>
    <div class="login">
        <div class="mar">
        <div class="loginbox">
            <h1>Login</h1><br>
            <form type="text" class="form">
                <input type="text" placeholder="Scan QR code...">
            </form>
            <button class="loginButton">
                <NuxtLink to="/personalDashboard">Anmelden</NuxtLink>
            </button>
            </div>
        </div>
    </div>
</template>

<style scoped>
.loginbox {
    width: 37%;
    height: 60vh;
    margin: auto;
    margin-top: 20vh;
    border-radius: 10px;
    background-color: white;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    filter: drop-shadow(0px 0px 7px rgb(201, 201, 201));
}

@media only screen and (max-width: 1444px) 
{
    .loginbox {
        width: 100%;
    }
}

.mar { 
    margin-inline: 12vw;
}
h1 {
    font-size: 2.6rem;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    margin-bottom: 7vh;
}
.form {
    width: 80%;
    display: flex;
    justify-content: center;
}
.form > input {
    width: 100%;
    border: 1px solid rgb(180, 180, 180);
    border-radius: 5px;
    padding-inline-start: 10px;
    margin-bottom: 5vh;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    font-size: 1.5rem;
    outline: none;
}

.form > input:focus {
    outline: 2px solid rgba(125, 169, 252, 0.747);
    filter: drop-shadow(0px 0px 3px rgb(125, 169, 252, 0.747));
}

.loginButton {
    all: unset;
    width: 80%;
    background-color: rgb(47, 116, 219);
    transition: background-color 0.2s;
    color: white;
    border-radius: 5px;
    margin-bottom: 22vh;
    padding-top: 12px;
    padding-bottom: 12px;
    display: flex;
    justify-content: center;
}

.loginButton > a {
    all: unset;
    font-weight: 500;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    font-size: 1.5rem;
}

.loginButton:hover {
    background-color: rgb(41, 86, 153);
    cursor: pointer;
}
</style>