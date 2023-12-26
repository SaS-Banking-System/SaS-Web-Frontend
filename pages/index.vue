<template>
    <div class="wrapper">
        <Navbar />
        <div class="hero">
            <h1>Die Bank der Bänke.</h1>
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
        opacity: 0%;
        transform: translateX(-60%);
    }
    100% {
        opacity: 100%;
        transform: translateX(0);
    }
}

h1 {
    display: flex;
    align-items: center;

    margin-top: 35vh;

    margin-left: 17.5rem;

    animation: 1s ease 0s 1 slideInFromLeft;

    font-size: 4.5rem;
    font-weight: 600;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    color: white;
} 

</style>
