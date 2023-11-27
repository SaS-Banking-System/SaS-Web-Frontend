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
    height: 8vh;
  }
  .left, .right {
    display: flex;
    align-items: center;
    margin-inline: 16rem;
  }

  a {
    all: unset;
    cursor: pointer;
    font-size: 1.2rem;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  }

  .left a {
    margin-inline: 1.5rem;
    background-image: linear-gradient(rgb(204, 50, 191),rgb(204, 50, 191));
    background-size: 0% 2px;
    background-position: 0% 100%;
    background-repeat: no-repeat;
    transition: background-size 0.17s, color 0.17s;
    color: rgb(0,0,0);
    padding: 3px;
  }
  .left a:hover {
    color: rgb(179, 22, 158);
    background-size: 100% 2px;
  }

  .login {
    border: solid 2px rgba(13, 124, 250, 0.616);
    transition: background 0.1s;
    color: rgba(13, 124, 250);
    font-size: 1rem;
    padding: 10px;
    border-radius: 5px;
  }

  .login:hover {
    background: rgba(13, 155, 250, 0.123);
  }
</style>