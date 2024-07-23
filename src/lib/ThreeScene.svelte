<script>
    import { onMount } from 'svelte';
    import * as THREE from 'three';
    import { GLTFLoader } from 'three/examples/jsm/loaders/GLTFLoader.js';
  
    let container;
  
    onMount(() => {
      // Scene
      const scene = new THREE.Scene();
  
      // Camera
      const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
      camera.position.z = 4;
  
      // Renderer
      const renderer = new THREE.WebGLRenderer({ alpha: true });
      renderer.setSize(window.innerWidth, window.innerHeight);
      container.appendChild(renderer.domElement);
  
      // Load 3D model
      const loader = new GLTFLoader();
      loader.load('/models/android.gltf', (gltf) => {
        scene.add(gltf.scene);
        animate();
        gltf.scene.traverse((child)=>{
            if (child.isMesh) {
            child.material.color.set(0x00ff00); 
            }
        })        
      }, undefined, (error) => {
        console.error(error);
      });
  
      // Animation loop
      function animate() {
        requestAnimationFrame(animate);
        // Rotate the model for some basic animation
        if (scene.children[0]) {
          scene.children[0].rotation.y += 0.01;
        }
        renderer.render(scene, camera);
      }
      const light_1 = new THREE.DirectionalLight(0xffffff, 1);
      const light_2 = new THREE.DirectionalLight(0xffffff, 1);
      
        light_1.position.set(1, 1, 1).normalize();
        light_2.position.set(0,1,1).normalize();

        scene.add(light_1,light_2);


      // Handle window resize
      window.addEventListener('resize', () => {
        camera.aspect = window.innerWidth / window.innerHeight;
        camera.updateProjectionMatrix();
        renderer.setSize(window.innerWidth, window.innerHeight);
      });
    });
  </script>
  
  <style>
    :global(body) {
      margin: 0;
      
    }
  
    div#container {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      z-index: -1; /* Place the canvas in the background */
    }
  </style>
  
  <div id="container" bind:this={container}></div>
  