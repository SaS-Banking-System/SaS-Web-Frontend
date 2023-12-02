<template>
    <div class="wrapper">
        <div class="logo-wrapper">
            <NuxtLink to="/">Logo</NuxtLink>
        </div>
        
        <Login class="login"></Login>
    </div>
</template>

<style scoped>
a {
    all: unset;
    cursor: pointer;
    font-size: 1.8rem;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.logo-wrapper {
    margin-left: 2rem;
    margin-top: 1rem;
}

</style>