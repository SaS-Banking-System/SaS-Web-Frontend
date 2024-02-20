<template>
  <nav>
  <div class="mar">
    <div class="left">
      <NuxtLink to="/">Logo</NuxtLink>
      <NuxtLink to="/faq">FAQ</NuxtLink>
      <NuxtLink to="/impressum">Impressum</Nuxtlink>
      <NuxtLink to="/checkout-login">Kasse</Nuxtlink>
    </div>
    <div class="right">
      <NuxtLink to="/login" class="loginLink">
        <button class="loginButton">Mein Konto</button>
      </NuxtLink>
    </div>
   </div>
  </nav>
</template>

<style scoped>
  nav {
    border-bottom: 2px solid rgb(194, 194, 194);
    background-color: white;
    height: 7vh;
    padding-top: 1.5vh;
  }

  .mar {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    margin-inline: 16rem;
  }

  .left, .right {
    display: flex;
    align-items: center;
  }

  a {
    all: unset;
    cursor: pointer;
    color: black;
    font-size: 1.2rem;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  }

  .left a {
    margin-inline: 1.5rem;
    background-image: linear-gradient(rgb(240, 124, 230), rgb(240, 124, 230));
    background-size: 0% 2px;
    background-position: 0% 100%;
    background-repeat: no-repeat;
    transition: background-size 0.17s, color 0.17s;
    font-weight: 600;
    padding: 3px;
  }
  .left a:hover {
    color: rgb(211, 100, 202);
    background-size: 100% 2px;
  }

  .loginButton {
    all: unset;
    border: solid 4px rgb(13, 124, 250);
    transition: background-color 0.1s;
    padding: 10px;
    border-radius: 5px;
  }

  .loginLink {
    color: rgba(13, 124, 250);
    font-size: 1rem;
    font-weight: 700;
  }

  .loginButton:hover {
    cursor: pointer;
    background-color: rgba(13, 155, 250, 0.123);
  }
</style>