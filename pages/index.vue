<template>
    <div class="wrapper">
        <Navbar />
        <div class="pageContent">
            <h1>Die Bank der Bänke.</h1>
            <div class="subheader">
                <p>Schnell,</p>
                <p>effizient</p>
                <p>und einfach.</p>
            </div>
        </div>
    </div>
</template>

<style scoped>
.wrapper {
    width: 100%;
    height: 100vh;
    background-color: rgb(10,10,10);
}

@keyframes slideInFromLeft {
    0% {
        transform: translateX(-60%);
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
    margin-top: 25vh;
    margin-bottom: -5vh;
    margin-left: 17.5rem;

    animation: 1s ease 0s 1 slideInFromLeft;
    animation-fill-mode: forwards;
    opacity: 0%;

    font-size: 4.5rem;
    font-weight: 600;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    color: white;
} 

p {
    margin-left: 17.5rem;
    margin-bottom: -3rem;

    animation: 0.9s ease 0.1s 1 slideInFromLeft;
    animation-fill-mode: forwards;
    opacity: 0%;

    font-size: 3rem;
    font-weight: 400;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    color: white;
} 

p:nth-child(2) {
    animation-delay: 0.2s;
    animation-duration: 0.8s;
}

p:nth-child(3) {
    animation-delay: 0.3s;
    animation-duration: 0.7s;
}

</style>
