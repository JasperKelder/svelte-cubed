<script>
	import * as THREE from 'three';
	import * as SC from 'svelte-cubed';
	import { TroisProvider } from 'svelte-trois';
	import { MouseEvents } from 'svelte-trois';

	let castleColor = false;

	const onClick = (e) => {
		e.stopPropagation();
		castleColor = !castleColor;
		confetti();
	};

	const castle = (e) => {
		e.stopPropagation();
		castleColor = !castleColor;
		confetti();
	};

	const tower1 = (e) => {
		e.stopPropagation();
	};

	const tower2 = (e) => {
		e.stopPropagation();
	};

	const tower3 = (e) => {
		e.stopPropagation();
	};

	const tower4 = (e) => {
		e.stopPropagation();
	};
</script>

<SC.Canvas antialias background={new THREE.Color('skyblue')} shadows>
	<TroisProvider>
		<SC.Group position={[0, -1, 0]}>
			<SC.Mesh
				geometry={new THREE.PlaneGeometry(20, 20)}
				material={new THREE.MeshStandardMaterial({ color: 'black' })}
				rotation={[-Math.PI / 2, 0, 0]}
				receiveShadow
			/>
			<SC.Primitive object={new THREE.GridHelper(19, 19, 'red', 'red')} position={[0, 0.001, 0]} />
		</SC.Group>

		{#if !castleColor}
			<MouseEvents {onClick}>
				<SC.Mesh
					geometry={new THREE.BoxGeometry()}
					material={new THREE.MeshStandardMaterial({ color: 0x023047 })}
					scale={[4, 2.5, 4]}
					castShadow
					position={[0, 0, 0]}
				/>
			</MouseEvents>
		{/if}

		{#if castleColor}
			<MouseEvents {onClick}>
				<SC.Mesh
					geometry={new THREE.BoxGeometry()}
					material={new THREE.MeshStandardMaterial({ color: 0x219ebc })}
					scale={[4, 2.5, 4]}
					castShadow
					position={[0, 0, 0]}
				/>
			</MouseEvents>
		{/if}

		<SC.Group position={[2, 0.5, 2]}>
			<SC.Mesh
				geometry={new THREE.CylinderGeometry()}
				material={new THREE.MeshStandardMaterial({ color: 0x023047 })}
				scale={[1, 3, 1]}
				castShadow
				position={[0, 0, 0]}
			/>
			<SC.Mesh
				geometry={new THREE.ConeGeometry()}
				material={new THREE.MeshStandardMaterial({ color: 0x023047 })}
				scale={[1, 1, 1]}
				castShadow
				position={[0, 2, 0]}
			/>
		</SC.Group>

		<SC.Group position={[2, 0.5, -2]}>
			<SC.Mesh
				geometry={new THREE.CylinderGeometry()}
				material={new THREE.MeshStandardMaterial({ color: 0x023047 })}
				scale={[1, 3, 1]}
				castShadow
				position={[0, 0, 0]}
			/>
			<SC.Mesh
				geometry={new THREE.ConeGeometry()}
				material={new THREE.MeshStandardMaterial({ color: 0x023047 })}
				scale={[1, 1, 1]}
				castShadow
				position={[0, 2, 0]}
			/>
		</SC.Group>

		<SC.Group position={[-2, 0.5, 2]}>
			<SC.Mesh
				geometry={new THREE.CylinderGeometry()}
				material={new THREE.MeshStandardMaterial({ color: 0x023047 })}
				scale={[1, 3, 1]}
				castShadow
				position={[0, 0, 0]}
			/>
			<SC.Mesh
				geometry={new THREE.ConeGeometry()}
				material={new THREE.MeshStandardMaterial({ color: 0x023047 })}
				scale={[1, 1, 1]}
				castShadow
				position={[0, 2, 0]}
			/>
		</SC.Group>

		<SC.Group position={[-2, 0.5, -2]}>
			<SC.Mesh
				geometry={new THREE.CylinderGeometry()}
				material={new THREE.MeshStandardMaterial({ color: 0x023047 })}
				scale={[1, 3, 1]}
				castShadow
				position={[0, 0, 0]}
			/>
			<SC.Mesh
				geometry={new THREE.ConeGeometry()}
				material={new THREE.MeshStandardMaterial({ color: 0x023047 })}
				scale={[1, 1, 1]}
				castShadow
				position={[0, 2, 0]}
			/>
		</SC.Group>

		<SC.PerspectiveCamera position={[10, 10, 10]} />
		<SC.OrbitControls enableZoom={true} maxPolarAngle={Math.PI * 0.5} />
		<SC.AmbientLight intensity={0.6} />
		<SC.DirectionalLight intensity={0.6} position={[-2, 3, 2]} shadow={{ mapSize: [2048, 2048] }} />
	</TroisProvider>
</SC.Canvas>
