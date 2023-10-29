<script lang="ts">
	import { onMount } from 'svelte';
	import TopAppBar, { Row, Section, Title, AutoAdjust } from '@smui/top-app-bar';
	import IconButton, { Icon } from '@smui/icon-button';
	import Button, { Label } from '@smui/button';

	let topAppBar: TopAppBar;
	let darkTheme: boolean;
	let defaultDarkMode = false;

	onMount(() => {
		darkTheme = window.matchMedia('(prefers-color-scheme: dark)').matches;
	});

	function toggleDarkMode() {
		darkTheme = !darkTheme;
	}
</script>

<svelte:head>
	{#if darkTheme}
		<link rel="stylesheet" href="/smui-dark.css" media="screen" />
	{:else if !darkTheme}
		<link rel="stylesheet" href="/smui.css" />
	{:else}
		<link rel="stylesheet" href="/smui.css" media="(prefers-color-scheme: light)" />
		<link rel="stylesheet" href="/smui-dark.css" media="screen and (prefers-color-scheme: dark)" />
	{/if}
</svelte:head>

<TopAppBar bind:this={topAppBar} variant="standard">
	<Row>
		<Section>
			<IconButton class="material-icons">menu</IconButton>
			<Title>Juan Gustavo Rueda Escobedo</Title>
		</Section>
		<Section align="end" toolbar>
			<!-- 			<IconButton class="material-icons" aria-label="Download">file_download</IconButton>
			<IconButton class="material-icons" aria-label="Print this page">print</IconButton>
			<IconButton class="material-icons" aria-label="Bookmark this page">bookmark</IconButton> -->
			<IconButton on:click={() => (darkTheme = !darkTheme)} toggle bind:pressed={defaultDarkMode}>
				<Icon class="material-icons" on>dark_mode</Icon>
				<Icon class="material-icons">light_mode</Icon>
			</IconButton>
		</Section>
	</Row>
</TopAppBar>
<AutoAdjust {topAppBar}>
	<slot />
</AutoAdjust>

<style>
	/* Hide everything above this component. */
	:global(#smui-app),
	:global(body),
	:global(html) {
		display: block !important;
		height: auto !important;
		width: auto !important;
		position: static !important;
	}

</style>
