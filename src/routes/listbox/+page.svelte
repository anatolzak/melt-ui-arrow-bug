<script lang="ts">
	import { createCombobox, melt, type ComboboxOptionProps } from '@melt-ui/svelte';

	type Manga = {
		author: string;
		title: string;
		disabled: boolean;
	};

	let mangas: Manga[] = [
		{
			author: 'Kentaro Miura',
			title: 'Berserk',
			disabled: false
		},
		{
			author: 'ONE',
			title: 'Mob Psycho 100',
			disabled: false
		},
		{
			author: 'Hajime Isayama',
			title: 'Attack on Titan',
			disabled: false
		},
		{
			author: 'Junji Ito',
			title: 'Uzumaki',
			disabled: false
		},
		{
			author: 'Yomi Sarachi',
			title: 'Steins Gate',
			disabled: false
		},
		{
			author: 'Tite Kubo',
			title: 'Bleach',
			disabled: false
		},
		{
			author: 'Masashi Kishimoto',
			title: 'Naruto',
			disabled: true
		},
		{
			author: 'Katsura Hoshino',
			title: 'D.Gray Man',
			disabled: false
		},
		{
			author: 'Tsugumi Ohba',
			title: 'Death Note',
			disabled: false
		},
		{
			author: 'Hiromu Arakawa',
			title: 'Fullmetal Alchemist',
			disabled: false
		}
	];

	const toOption = (manga: Manga): ComboboxOptionProps<Manga> => ({
		value: manga,
		label: manga.title,
		disabled: manga.disabled
	});

	const {
		elements: { menu, input, option, label, arrow },
		states: { open, inputValue, touchedInput, selected }
	} = createCombobox<Manga>({
		arrowSize: 8,
		positioning: { gutter: 10, placement: 'bottom' }
	});

	$: if (!$open) {
		$inputValue = $selected?.label ?? '';
	}

	$: filteredMangas = $touchedInput
		? mangas.filter(({ title, author }) => {
				const normalizedInput = $inputValue.toLowerCase();
				return (
					title.toLowerCase().includes(normalizedInput) ||
					author.toLowerCase().includes(normalizedInput)
				);
			})
		: mangas;
</script>

<div class="flex flex-col gap-1">
	<!-- svelte-ignore a11y-label-has-associated-control - $label contains the 'for' attribute -->
	<label use:melt={$label}>
		<span class="text-sm font-medium text-blue-400">Choose your favorite manga:</span>
	</label>

	<div class="relative">
		<input
			use:melt={$input}
			class="flex h-10 items-center justify-between rounded-lg bg-white
					px-3 pr-12 text-black"
			placeholder="Best book ever"
		/>
	</div>
</div>
<ul class="force-dark z-10 flex max-h-[300px] flex-col rounded-lg bg-blue-400" use:melt={$menu}>
	<div use:melt={$arrow} />
	<!-- svelte-ignore a11y-no-noninteractive-tabindex -->
	<div class="flex max-h-full flex-col gap-0 overflow-y-auto px-2 py-2 text-black" tabindex="0">
		{#each filteredMangas as manga, index (index)}
			<li
				use:melt={$option(toOption(manga))}
				class="relative cursor-pointer scroll-my-2 rounded-md py-2 pl-4 pr-4
				hover:bg-blue-100
				data-[highlighted]:bg-blue-200 data-[highlighted]:text-white
					data-[disabled]:opacity-50"
			>
				<div class="pl-4">
					<span class="font-medium">{manga.title}</span>
					<span class="block text-sm opacity-75">{manga.author}</span>
				</div>
			</li>
		{:else}
			<li class="relative cursor-pointer rounded-md py-1 pl-8 pr-4">No results found</li>
		{/each}
	</div>
</ul>
