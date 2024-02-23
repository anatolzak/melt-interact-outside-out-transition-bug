<script lang="ts">
	import '../app.pcss';
	import { page } from '$app/stores';
	import { afterNavigate } from '$app/navigation';

	const links: { href: string; label: string }[] = [
		{
			href: '/',
			label: 'popover'
		},
		{
			href: '/menu',
			label: 'menu'
		},
		{
			href: '/date-range-picker',
			label: 'date range picker'
		},
		{
			href: '/date-picker',
			label: 'date picker'
		},
		{
			href: '/link-preview',
			label: 'link preview'
		},
		{
			href: '/tooltip',
			label: 'tooltip'
		},
		{
			href: '/combobox',
			label: 'combobox'
		},
		{
			href: '/select',
			label: 'select'
		}
	];

	afterNavigate(() => {
		mounted = true;
	});

	let mounted = true;
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
		<button
			class="ring-offset-background focus-visible:ring-ring border-input bg-background hover:bg-accent hover:text-accent-foreground inline-flex h-10 items-center justify-center whitespace-nowrap rounded-md border px-4 py-2 text-sm font-medium transition-colors focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-offset-2 disabled:pointer-events-none disabled:opacity-50"
			on:click={() => (mounted = !mounted)}
		>
			{mounted ? 'unmount' : 'mount'}
		</button>
		{#if mounted}
			<slot />
		{/if}
	</div>
</div>
