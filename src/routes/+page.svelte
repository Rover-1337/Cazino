<script lang="ts">
	import { Button } from '$lib/components/ui/button';
	import { onMount } from 'svelte';
	import { loading, progress } from '$lib/store';
	import { get } from 'svelte/store';

	progress.set(33);
	const Chart = import('$lib/components/Chart.svelte').then((module) => module.default);
	onMount(() => {
		setTimeout(() => {
			progress.set(100);
			setTimeout(() => {
				loading.set(false);
			}, 1000);
		}, 1000);
	});
</script>

<div class="mx-auto flex w-4/6 items-center justify-center">
	<div>
		<h1 class="w-3/4 scroll-m-20 text-4xl font-extrabold tracking-tight lg:text-5xl">
			Spinergy Redefine Your Game
		</h1>

		<div class="mt-4 text-lg font-medium text-gray-500">
			Spinergy is a platform that helps you to redefine your game by providing you with the best
			tools to improve your performance.
		</div>
		<div class="mt-4 flex">
			<Button class="">Start Now</Button>
			<Button class="ml-4" variant="outline">Explore</Button>
		</div>
	</div>
	<div class="scale-75">
		{#await Chart then ChartComponent}
			<ChartComponent />
		{/await}
	</div>
</div>
