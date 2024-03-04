<script lang="ts">
	import { page } from '$app/stores';
	import '../app.pcss';

	const links: { href: string; label: string }[] = [
		{
			href: '/',
			label: 'tooltip'
		},
		{
			href: '/listbox',
			label: 'listbox'
		},
		{
			href: '/popover',
			label: 'popover'
		}
	];
</script>

<div class="h-full bg-gray-100 p-10">
	<div class="flex space-x-3 py-4">
		{#each links as { href, label }}
			{@const isActive = $page.url.pathname === href}
			<a class={` ${isActive ? 'border-b border-b-gray-800' : 'text-gray-500'}`} {href}>
				{label}
			</a>
		{/each}
	</div>
	<div>
		<slot />
	</div>
</div>
