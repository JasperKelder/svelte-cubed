<script>
	import * as THREE from 'three';
	import * as SC from 'svelte-cubed';
	import { TroisProvider } from 'svelte-trois';
	import { MouseEvents } from 'svelte-trois';

	let width = 1;
	let height = 1;
	let depth = 1;

	let spin = 0;

	SC.onFrame(() => {
		spin += 0.005;
	});

	const onClick = (e) => {
		e.stopPropagation();
	};
</script>

<svelte:head>
	<title>Svelte Cubed</title>
</svelte:head>

<header>Hallo</header>

<SC.Canvas antialias background={new THREE.Color('skyblue')} shadows>
	<TroisProvider>
		<SC.Group position={[0, -height / 2, 0]}>
			<SC.Mesh
				geometry={new THREE.PlaneGeometry(15, 15)}
				material={new THREE.MeshStandardMaterial({ color: 'black' })}
				rotation={[-Math.PI / 2, 0, 0]}
				receiveShadow
			/>
			<SC.Primitive object={new THREE.GridHelper(14, 14, 'red', 'red')} position={[0, 0.001, 0]} />
		</SC.Group>

		<MouseEvents {onClick}>
			<SC.Mesh
				geometry={new THREE.BoxGeometry()}
				material={new THREE.MeshStandardMaterial({ color: 0x023047 })}
				scale={[width, height, depth]}
				rotation={[0, spin, 0]}
				castShadow
			/>
		</MouseEvents>

		<SC.PerspectiveCamera position={[1, 1, 3]} />
		<SC.OrbitControls enableZoom={true} maxPolarAngle={Math.PI * 0.5} />
		<SC.AmbientLight intensity={0.6} />
		<SC.DirectionalLight intensity={0.6} position={[-2, 3, 2]} shadow={{ mapSize: [2048, 2048] }} />
	</TroisProvider>
</SC.Canvas>

<div class="controls">
	<label><input type="range" bind:value={width} min={0.1} max={3} step={0.1} /> Width</label>
	<label><input type="range" bind:value={height} min={0.1} max={3} step={0.1} /> Height</label>
	<label><input type="range" bind:value={depth} min={0.1} max={3} step={0.1} /> Depth</label>
</div>

<div class="left" />
<div class="right" />
<footer />

<style>
	*,
	*::after,
	*::before {
		margin: 0;
		padding: 0;
		box-sizing: inherit;
		box-sizing: border-box;
		z-index: 1;
	}

	.controls {
		position: absolute;
		right: 50%;
		top: 2em;
	}

	label {
		display: flex;
		width: 60px;
		gap: 1.5em;
		align-items: center;
		color: white;
	}

	input {
		width: 200px;
		margin: 0;
	}

	header,
	footer {
		width: 100vw;
		height: 10vh;
		background-color: black;
		position: absolute;
		left: 0;
	}

	header {
		top: 0;
		border-bottom: 2px solid red;
	}

	footer {
		bottom: 0;
		border-top: 2px solid red;
	}

	.left,
	.right {
		height: 100vh;
		background-color: black;
		position: absolute;
		top: 0;
		width: 10vw;
	}

	.right {
		right: 0;
		border-left: 2px solid red;
	}

	.left {
		left: 0;
		border-right: 2px solid red;
	}
</style>
