<script lang="ts">
	import { createTooltip, melt } from '@melt-ui/svelte';
	import { fade } from 'svelte/transition';

	const {
		elements: { trigger, content, arrow }
	} = createTooltip({
		positioning: {
			placement: 'bottom',
			gutter: 10
		},
		openDelay: 0,
		closeDelay: 0
	});
</script>

<button type="button" class="trigger" use:melt={$trigger} aria-label="Add"> Open tooltip </button>

<div use:melt={$content} class="force-dark z-10 rounded-lg bg-blue-400 shadow">
	<div use:melt={$arrow} />
	<p class="px-4 py-1 text-white">Add item to library</p>
</div>

<style lang="postcss">
	.trigger {
		@apply inline-flex items-center justify-center rounded-full bg-blue-400 px-3 py-1;
		@apply text-white transition-colors hover:bg-blue-400/90;
		@apply focus-visible:ring focus-visible:ring-blue-400 focus-visible:ring-offset-2;
		@apply font-medium;
	}
</style>
