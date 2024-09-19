<!-- <script context="module">
	export async function load({ session }) {
		if (session.user) {
			return {
				status: 302,
				redirect: '/'
			};
		}
		return {};
	}
</script>

<script lang="ts">
	import { session } from '$app/stores';
	import { goto } from '$app/navigation';
	import { Alert } from 'flowbite-svelte';
	// Variables bound to respective inputs via bind:value
	let name: string;
	let email: string;
	let error: string;
	// let notice
	const login = async () => {
		// Reset error from previous failed attempts
		error = undefined;
		// POST method to src/routes/auth/login.js endpoint
		try {
			const res = await fetch('/auth/api/login', {
				method: 'POST',
				body: JSON.stringify({
					name,
					email
				}),
				headers: {
					'Content-Type': 'application/json'
				}
			});
			if (res.ok) {
				const data = await res.json();
				$session.user = data.user;
				goto('/');
			} else {
				const data = await res.json();
				error = `LOS001: ${data.message}`;
			}
		} catch (err) {
			console.log(err);
			error = 'LOS002: Pleas try it again.';
		}
	};
</script> -->

<script lang="ts">
    // Variables bound to respective inputs via bind:value
	let name: string;
	let email: string;
    let error: string;

    async function getData() {
        const url = "https://frontend-take-home-service.fetch.com/login";
        try {
            const response = await fetch(url);
            if (!response.ok) {
                throw new Error(`Response status: ${response.status}`);
            }
            const json = await response.json();
            console.log(json);
        } catch (e: any) {
            console.error(e.message);
        }
    }
</script>

<div class="container mt-4 flex flex-wrap justify-center mx-auto pt-16">
	<div
		class="p-4 max-w-sm bg-white rounded-lg border border-gray-200 shadow-md sm:p-6 lg:p-8 dark:bg-gray-800 dark:border-gray-700 w-full"
	>
		<form class="space-y-6">  <!-- on:submit|preventDefault={login} -->
			<div class="heading">
				<a class="back" href="/"><i class="bi bi-arrow-left dark:text-white" /></a>
				<h2 class="text-xl font-medium text-gray-900 dark:text-white">Login</h2>
			</div>
            <div>
				<label
					for="name"
					class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-300"
					>Your name</label
				>
				<input
					type="text"
					required
					name="name"
					placeholder="Enter your name"
					bind:value={name}
					class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-600 dark:border-gray-500 dark:placeholder-gray-400 dark:text-white"
				/>
			</div>
			<div>
				<label for="email" class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-300"
					>Email</label
				>
				<input
					type="email"
					required
					name="email"
					placeholder="Enter your email"
					bind:value={email}
					class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-600 dark:border-gray-500 dark:placeholder-gray-400 dark:text-white"
				/>
			</div>
			<!-- {#if error}
				<div class="mt-6">
					<Alert alertId="alert-red" color="red" closeBtn>
						{error}
					</Alert>
				</div>
			{/if} -->
			<button
                type="submit"
                class="w-full text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
                on:click={getData}
            >
                Log in
            </button>
		</form>
	</div>
</div>

<!-- <svelte:head>
	<title>Login</title>
</svelte:head> -->