<script>
  import { T } from '@threlte/core';
  import { GLTF, OrbitControls, interactivity } from '@threlte/extras';
  interactivity();
</script>

<T.DirectionalLight position={[3, 10, 10]} />
<T.AmbientLight intensity={0.5} />

<!--Don't use <Align> elements as it doesn't display the 3D model-->
<T.Group position={[0, -0.5, 0]}>
    <GLTF 
      url="/models/Duck.glb" 
      interactive
    />
</T.Group>

<T.PerspectiveCamera makeDefault position={[8, 8, -16]} fov={12}>
<OrbitControls enableDamping />
</T.PerspectiveCamera>
