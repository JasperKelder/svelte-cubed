<script>
	import Canvas from '$lib/Canvas.svelte';

	let openCanvas = false;
</script>

<svelte:head>
	<title>Svelte Cubed</title>
</svelte:head>

<Canvas />
<header>
	<h1 on:click={() => (openCanvas = !openCanvas)}>Svelte Cubed</h1>
</header>
<div class="left" class:openCanvas />
<div class="right" class:openCanvas />

<style>
	:root {
		--white: #ffffff;
		--black: #023047;
		--yellow: #ffb703;
		--blue: #219ebc;
	}

	*,
	*::after,
	*::before {
		margin: 0;
		padding: 0;
		box-sizing: inherit;
		box-sizing: border-box;
		z-index: 1;
	}

	header {
		width: 100vw;
		height: 10vh;
		background-color: var(--black);
		position: absolute;
		left: 0;
		top: 0;
		border-bottom: 2px solid var(--blue);
	}

	.left,
	.right {
		height: 90vh;
		background-color: var(--black);
		position: absolute;
		top: 10vh;
		width: 50vw;
		transition: width 0.4s;
	}

	.right {
		right: 0;
		border-left: 1px solid var(--blue);
	}

	.left {
		left: 0;
		border-right: 1px solid var(--blue);
	}

	h1 {
		position: absolute;
		top: 40px;
		left: 50%;
		transform: translate(-50%);
		color: var(--blue);
		transition: color 0.4s;
		cursor: pointer;
	}

	h1:hover {
		color: var(--yellow);
	}

	.openCanvas {
		width: 0;
		border: none;
	}
</style>
