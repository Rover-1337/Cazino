<script lang="ts">
	import * as Sheet from '$lib/components/ui/sheet';
	import { AlignJustify, ChartLine } from 'lucide-svelte';
</script>

<Sheet.Root>
	<Sheet.Trigger><AlignJustify class="h-8 w-8" /></Sheet.Trigger>
	<Sheet.Content side="left">
		<Sheet.Header>
			<Sheet.Close class="w-full">
				<Sheet.Title class="text-center"
					><a href="/" class="text-2xl font-bold">Spinergy</a></Sheet.Title
				></Sheet.Close
			>
			<Sheet.Description>
				<Sheet.Close class="w-full">
					<a href="/crash">
						<div
							class="my-4 flex items-center gap-4 rounded-lg border border-primary-foreground p-4 duration-100 hover:text-white"
						>
							<ChartLine />
							<div class="h-8 border-2 border-l border-green-600"></div>
							<h4 class="scroll-m-20 text-xl font-semibold tracking-tight">Crash</h4>
						</div></a
					></Sheet.Close
				>
			</Sheet.Description>
		</Sheet.Header>
	</Sheet.Content>
</Sheet.Root>
