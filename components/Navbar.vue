<template>
  <nav>
   <div class="left">
     <NuxtLink to="/" class="logo">Logo</NuxtLink>
     <NuxtLink to="/faq" class="faq">FAQ</NuxtLink>
     <NuxtLink to="/impressum" class="impressum">Impressum</Nuxtlink>
   </div>
   <div class="right">
     <NuxtLink to="/login" class="login">Mein Konto</NuxtLink>
   </div>
  </nav>
</template>

<style scoped>
  nav {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    background-color: white;
    height: 8vh;
    margin-inline: 8rem;
  }
  .left, .right {
    display: flex;
    align-items: center;
  }

  a {
    all: unset;
    cursor: pointer;
    font-size: 1.2rem;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  }

  .left a {
    margin-inline: 1.5rem;
    background-image: linear-gradient(rgb(211, 100, 202), rgb(211, 100, 202));
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
