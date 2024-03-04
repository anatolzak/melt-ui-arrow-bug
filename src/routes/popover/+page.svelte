<script lang="ts">
	import { createPopover, melt } from '@melt-ui/svelte';

	const {
		elements: { trigger, content, arrow }
	} = createPopover({ positioning: { gutter: 10, placement: 'bottom' } });
</script>

<button type="button" class="trigger" use:melt={$trigger} aria-label="Update dimensions">
	<span>Open Popover</span>
</button>

<div use:melt={$content} class="force-dark content">
	<div use:melt={$arrow} />
	<div class="flex flex-col gap-2.5">
		<p>Dimensions</p>
	</div>
</div>

<style lang="postcss">
	p {
		@apply text-white mb-2 font-medium;
	}

	.trigger {
		@apply inline-flex items-center justify-center rounded-full bg-blue-400 px-3 py-1;
		@apply text-white font-medium transition-colors hover:bg-blue-400/90;
		@apply focus-visible:ring focus-visible:ring-blue-400 focus-visible:ring-offset-2;
	}

	.content {
		@apply z-10 w-60 rounded-[4px] bg-blue-400 p-5 shadow-sm;
	}
</style>
