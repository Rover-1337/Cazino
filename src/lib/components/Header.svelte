<script lang="ts">
	import { Button } from '$lib/components/ui/button';
	import Sidebar from './Sidebar.svelte';
</script>

<div class="flex items-center">
	<div class="ml-6 mt-5">
		<Sidebar />
	</div>
	<div class="mx-auto mt-4 flex w-5/6">
		<div class="flex flex-1 gap-3">
			<a href="/" class="text-2xl font-bold">Spinergy</a>
			<p class="-ml-2 mt-1 text-sm">&copy;</p>
		</div>
		<div class="flex flex-1 justify-end">
			<Button class="ml-4" variant="outline">Login</Button>
			<Button class="ml-4">Sign Up</Button>
		</div>
	</div>
</div>
