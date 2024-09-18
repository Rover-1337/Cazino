<script>
	import { loading, progress } from '$lib/store';
	import { Progress } from '$lib/components/ui/progress';
	// @ts-ignore
	import { ModeWatcher } from 'mode-watcher';
	import * as AlertDialog from '$lib/components/ui/alert-dialog';

	import Header from '$lib/components/Header.svelte';
	import '../app.css';

	let loadingdots = '...';
	setInterval(() => {
		loadingdots = loadingdots.length === 3 ? '' : loadingdots + '.';
	}, 500);
</script>

<ModeWatcher />

<AlertDialog.Root open={$loading}>
	<AlertDialog.Content class="border-none bg-transparent outline-none">
		<AlertDialog.Header>
			<AlertDialog.Description>
				<h4 class="-mb-4 translate-x-[42%] text-xl font-semibold tracking-tight text-white">
					Loading{loadingdots}
				</h4>
				<p class="mb-4 text-center leading-7 [&:not(:first-child)]:mt-6">
					Please wait while we load the page for you.
				</p>
				<Progress class="mx-auto w-1/2" value={$progress} />
			</AlertDialog.Description>
		</AlertDialog.Header>
	</AlertDialog.Content>
</AlertDialog.Root>
<Header />
<slot></slot>
