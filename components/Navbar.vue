<template>
  <nav>
   <div class="left">
     <a href="">Logo</a>
     <a href="">FAQ</a>
     <a href="">Impressum</a>
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
    height: 12vh;
  }
  .left, .right {
    display: flex;
    align-items: center;
    margin-inline: 10rem;
  }
  .left > a {
    margin-inline: 2rem;
  }
  a {
    all: unset; 
    cursor: pointer;
    font-size: 1.3rem;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  }
  .login {
    outline: 1px solid black;
    padding: 10px;
    border-radius: 10px;
  }
</style>