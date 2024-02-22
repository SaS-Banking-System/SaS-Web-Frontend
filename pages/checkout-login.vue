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
		background-color: white;
		filter: drop-shadow(0px 0px 7px rgb(201, 201, 201));
		padding: 50px;
		padding-top: 20px;
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
		font-size: 2.6rem;
		margin-bottom: 3rem;
		text-align: center;
		font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
	}

	input {
		all: unset;
		border: 1px solid rgb(180, 180, 180);
		border-radius: 5px;
		padding: 10px;
		font-size: 1.3rem;
		outline: none;
		font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
	}

	input:focus {
		outline: 2px solid rgba(125, 169, 252, 0.747);
	}

	.login-button {
		all: unset;
		font-size: 1.3rem;
		margin-left: 1.1rem;
		cursor: pointer;
		background-color: rgb(38, 189, 126);
		color: white;
		padding: 0.7rem;
		border-radius: 5px;
		font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
	}

	.login-button:hover {
		background-color: rgb(52, 156, 95);
	}

	.index-page-button {
		all: unset;
		display: flex;
		margin-top: 1.5rem;
		font-size: 1.3rem;
		font-weight: bold;
		margin-inline: auto;
		padding: 10px;
		border: 5px solid #2172f2;
		border-radius: 10px;
		cursor: pointer;
		background-color: white;
		transition: all 0.3s ease-in-out;
		font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
	}
	.index-page-button:hover {
		background-color: #2172f2;
		color: white;
	}
	.index-page-a {
		all: unset;
		color: #2172f2;
		transition: all 0.1s ease-in-out;
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