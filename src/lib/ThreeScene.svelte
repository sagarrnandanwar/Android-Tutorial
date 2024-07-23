<script>
    import { onMount } from 'svelte';
    import * as THREE from 'three';
    import { GLTFLoader } from 'three/examples/jsm/loaders/GLTFLoader.js';
  
    let container;
    let model;
    let elapsedTime;
    onMount(() => {
      const scene = new THREE.Scene();
  
      const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
      camera.position.z = 4;
      camera.position.y=0.05;
  
      const renderer = new THREE.WebGLRenderer({ alpha: true });
      renderer.setSize(window.innerWidth, window.innerHeight);
      container.appendChild(renderer.domElement);
  
      const loader = new GLTFLoader();
      loader.load('/models/AndroidBug.glb', (gltf) => {
        scene.add(gltf.scene);
        animate();
        gltf.scene.traverse((child)=>{
            if (child.isMesh) {
            // child.material.color.set(0x00ff00); 
            }
        })        
        model=gltf.scene;
      }, undefined, (error) => {
        console.error(error);
      });
  
      let startTime = Date.now();
      
      function animate() {
        requestAnimationFrame(animate);
        
        if (model) {
            elapsedTime = (Date.now() - startTime) / 1000;
            scene.children[2].position.y = Math.sin(elapsedTime) * 0.1;
        }
        renderer.render(scene, camera);
      }

      const light_1 = new THREE.DirectionalLight(0xffffff, 1.5);
      const light_2 = new THREE.DirectionalLight(0xffffff, 1.5);
      
        light_1.position.set(1, 1, 1).normalize();
        light_2.position.set(0,1,1).normalize();

        scene.add(light_1,light_2);


      window.addEventListener('resize', () => {
        camera.aspect = window.innerWidth / window.innerHeight;
        camera.updateProjectionMatrix();
        renderer.setSize(window.innerWidth, window.innerHeight);
      });

      window.addEventListener('scroll', () => {
      if (model) {
        scene.children[2].rotation.y = window.scrollY * -0.01;
      }
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
  
  <div id="container" style="background-image:url('/bg_2.png');background-position:center;" bind:this={container}></div>
  