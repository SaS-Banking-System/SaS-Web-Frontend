<template>
  <div class="wrapper">
    <Navbar />
    <div class="pageContent">
      <div class="header">
        <div class="subheader">
          <h1>Die Bank der Bänke.</h1>
          <p>Schnell,</p>
          <p>effizient</p>
          <p>und einfach.</p>
        </div>
        <img class="kreditkarte" src="/kreditkarte.png" alt="Credit Card" />
      </div>
    </div>
  </div>
</template>

<style scoped>
.header {
  display: flex;
  flex-direction: row;
}
.wrapper {
  width: 100%;
  height: 100vh;
  background-image: url("/gradientbackground.svg");
  background-repeat: no-repeat;
  background-size: cover;
}

.kreditkarte {
  margin-top: -7vh;
  scale: 0.7;
}

@keyframes slideInFromLeft {
  0% {
    transform: translateX(-100%);
  }
  100% {
    opacity: 100%;
    transform: translateX(0);
  }
}

.pageContent {
  display: flex;
  flex-direction: column;
}

.subheader {
  display: flex;
  flex-direction: column;
}

h1 {
  margin-top: 21vh;
  margin-bottom: -5vh;
  margin-left: 17.5rem;

  animation: 1s ease 0s 1 slideInFromLeft;
  animation-fill-mode: forwards;
  opacity: 0%;

  font-size: 4.5rem;
  font-weight: 600;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  color: black;
}

p {
  margin-left: 17.5rem;
  margin-bottom: -3rem;

  animation: 0.9s ease 0.1s 1 slideInFromLeft;
  animation-fill-mode: forwards;
  opacity: 0%;

  font-size: 3rem;
  font-weight: 400;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  color: black;
}

p:nth-child(3) {
  animation-delay: 0.2s;
  animation-duration: 0.8s;
}

p:nth-child(4) {
  animation-delay: 0.3s;
  animation-duration: 0.7s;
}
</style>
