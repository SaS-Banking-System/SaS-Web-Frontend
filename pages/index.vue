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
    width: 100vw;
    height: 130vh;
    background-color: white;
}

.hero {
    height: 92vh;
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
    justify-content: center;
    align-items: center;
    padding-top: 12%;
    margin-right: 53%;

    animation: 1s ease 0s 1 slideInFromLeft;

    font-size: 4.5rem;
    font-weight: 300;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}
</style>