<script lang="ts">
	import * as Card from '$lib/components/ui/card';
	import { loading, progress } from '$lib/store';
	import { onMount } from 'svelte';
	import { Input } from '$lib/components/ui/input';
	import { Button } from '$lib/components/ui/button';
	import { OrbitControls } from '@threlte/extras';

	import { Canvas } from '@threlte/core';
	import Model from '$lib/components/rocket.svelte';
	import { T } from '@threlte/core';

	progress.set(33);
	onMount(() => {
		setTimeout(() => {
			progress.set(100);
			setTimeout(() => {
				loading.set(false);
				// Start the crash animation after loading is complete
			}, 1000);
		}, 1000);
	});

	let loadingdots = '...';
	setInterval(() => {
		loadingdots = loadingdots.length === 3 ? '' : loadingdots + '.';
	}, 500);

	let crash = 1;
	let crashed = false;
	let crashpoint = 0;
	let started = false;
	let betsize: any = '';

	const animate = () => {
		crash += 0.001;
		requestAnimationFrame(animate);
	};

	function startBet() {
		crashpoint = Math.floor(Math.random() * 100) + 1;
		console.log(crashpoint);
		started = true;

		animate();
	}

	$: if (crashpoint <= crash && started) {
		crashed = true;
		started = false;
	} else {
		crashed = false;
	}
</script>

<Card.Root class="mx-auto mt-12 flex w-4/6">
	<div class="m-4 h-[600px] w-4/6 rounded border p-4">
		<Canvas>
			<T.PerspectiveCamera makeDefault position={[1000, 1000, 0]} near={10} far={10000}>
				<OrbitControls
					autoRotate
					autoRotateSpeed={1}
					enableDamping
					enableZoom={false}
					enablePan={false}
					target={[-60, -75, 5]}
				/>
			</T.PerspectiveCamera>
			<T.AmbientLight intensity={1} />
			<T.DirectionalLight intensity={0.5} position={[0, 0, 5]} />
			<Model />
		</Canvas>

		<div class=" mx-auto -mt-32 w-1/2 rounded-full border bg-white/80 p-4">
			{#if !started}
				<h1 class="mx-auto w-[18rem] text-6xl font-bold text-black">Waiting{loadingdots}</h1>
			{:else if crashed}
				<h1 class=" w-[24rem] text-6xl font-bold text-red-600">Crashed! @ {crash.toFixed(2)}x</h1>
			{:else}
				<h1 class=" w-[24rem] text-6xl font-bold text-green-600">Crash: {crash.toFixed(2)}x</h1>
				<p class="mt-2 text-center text-xl font-bold text-black">
					Cashout: {(betsize * crash).toFixed(2)}$
				</p>
			{/if}
		</div>
	</div>

	<div class="m-4 mx-auto py-3">
		<h1 class="mb-8 text-2xl font-bold">Place a bet</h1>
		<div class="flex flex-1">
			<Input class="ring- mb-4 w-[18rem] rounded-r-none" bind:value={betsize} />
			<Input class="mb-4 w-[3rem] rounded-l-none text-center" disabled value="$" />
		</div>

		{#if betsize > 0 && !started}
			<Button class="mb-8 w-full py-7 text-xl font-bold" on:click={startBet}>Start Bet</Button>
		{:else}
			<Button class="mb-8 w-full py-7 text-xl font-bold" disabled>Start Bet</Button>
		{/if}

		<Card.Root>
			<Card.Header>Crash History</Card.Header>
			<Card.Content>
				<div class="flex justify-between">
					<p>1.00x</p>
					<p>1000</p>
				</div>
				<div class="flex justify-between">
					<p>1.00x</p>
					<p>1000</p>
				</div>
				<div class="flex justify-between">
					<p>1.00x</p>
					<p>1000</p>
				</div>
				<div class="flex justify-between">
					<p>1.00x</p>
					<p>1000</p>
				</div>
				<div class="flex justify-between">
					<p>1.00x</p>
					<p>1000</p>
				</div>
			</Card.Content>
		</Card.Root>
	</div>
</Card.Root>
