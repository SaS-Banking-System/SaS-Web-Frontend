<template>
  <nav>
   <div class="left">
     <NuxtLink to="/" class="logo">Logo</NuxtLink>
     <NuxtLink to="/faq" class="faq">FAQ</NuxtLink>
     <NuxtLink to="/impressum" class="impressum">Impressum</Nuxtlink>
   </div>
   <div class="right">
     <a class="login" href="">Mein Konto</a>
   </div>
  </nav>
</template>

<style scoped>
  nav {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    height: 6vh;
  }
  .left, .right {
    display: flex;
    align-items: center;
    margin-inline: 16rem;
  }

  a {
    all: unset;
    cursor: pointer;
    font-size: 1.4rem;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  }

  .left a {
    margin-inline: 1.5rem;
    border-radius: 6px;
    padding: 10px;
  }
  .left a:hover {
    color: rgb(12, 68, 105);
    background-color: rgb(185, 221, 245);
  }
  .login {
    background: rgb(43, 43, 43);
    color: white;
    font-size: 1.2rem;
    padding: 5px;
    border-radius: 5px;
  }

  .login:hover {
    background: rgb(97, 97, 97);
  }
</style>