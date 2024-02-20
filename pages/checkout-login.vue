<script setup lang="ts">
let companyCode = ref<string>('')
let wrongCompanyCode = ref<boolean>(false)

if (useCookie('ccode') !== undefined) navigateTo('checkout')

async function login() {
	// trigger error animation
	if (!String(companyCode.value).match(/^[0-9]{2,4}$/g)) {
		wrongCompanyCode.value = true;
		return
	}

	const companyRequest = await useFetch(`http://localhost:3001/company/info/${companyCode.value}`)

  if (!companyRequest || companyRequest.status.value === 'error') { 
  	wrongCompanyCode.value = true;
  	return
  }

	const companyCodeCookie = useCookie('ccode');
	companyCodeCookie.value = companyCode.value;

	navigateTo('/checkout')
}
</script>

<template>
  <div class="wrapper">
	  <h1>Login für die Kasse</h1>
		<form @submit.prevent="login">
			<input v-model="companyCode" type="number" placeholder="Betriebsnummer" />
			<button class="login-button" type="submit">Einloggen</button>
			<p class="wrong-ccode" v-if="wrongCompanyCode">Der eingegebene Code konnte nicht gefunden werden</p>
		</form>
	  <a class="index-page-a" href="/"><button class="index-page-button">Zur Startseite</button></a>
  </div>
</template>

<style scoped>
	.wrapper {
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
	}
	.inputFieldError {
		border-color: red;
		animation-name: inputFieldErrorAnimation;
		animation-duration: 0.3s;
	}
	h1 {
		font-size: 2rem;
		margin-bottom: 2rem;
		text-align: center;
	}
	input {
		all: unset;
		border: 1px solid gray;
		border-radius: 3px;
		padding: 10px;
		font-size: 1.2rem;
	}
	.login-button {
		all: unset;
		font-size: 1.2rem;
		padding: 0.5rem;
		margin-left: 1.1rem;
		cursor: pointer;
		background-color: #29e88c;
		color: white;
		padding: 0.7rem;
		border-radius: 5px;
	}
	.index-page-button {
		all: unset;
		display: flex;
		margin-top: 1.5rem;
		font-size: 1.1rem;
		font-weight: bold;
		margin-inline: auto;
		padding: 10px;
		border: 5px solid #2172f2;
		border-radius: 10px;
		cursor: pointer;
		background-color: white;
		transition: all 0.3s ease-in-out;
	}
	.index-page-button:hover {
		background-color: #2172f2;
		color: white;
	}
	.index-page-a {
		all: unset;
		color: #2172f2;
		transition: all 0.3s ease-in-out;
	}
	.index-page-a:hover {
		color: white;
	}

	@keyframes inputFieldErrorAnimation {
		25% {
			transform: translateX(+10px);
		}
		75% {
			transform: translateX(-10px);
		}
		to {
			transform: translateX(0);
		}
	}
	.wrong-ccode {
    color: red;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    font-size: 1.7rem;
}
</style>e>