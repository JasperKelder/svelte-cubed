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
