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
    align-items: center;

    margin-top: 35vh;

    /* 9.5 rem because there are 8 rem margin on the navbar and 1.5 rem margin on the first a (Logo link) */
    margin-left: 9.5rem;

    animation: 1s ease 0s 1 slideInFromLeft;

    font-size: 4.5rem;
    font-weight: 300;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}
</style>
