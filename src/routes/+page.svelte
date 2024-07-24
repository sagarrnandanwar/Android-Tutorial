<script>
    import {onMount} from 'svelte'
    import Prism from 'prismjs';
    import ThreeScene from '../lib/ThreeScene.svelte';
    import 'prismjs/components/prism-javascript'; 
    import './prism-dark.css'
    import {Data} from "../lib/data"
    import Footer from '../lib/Footer.svelte';
    import Header from '../lib/Header.svelte';
    onMount(() => {
        Prism.highlightAll();
    });
</script>

<ThreeScene></ThreeScene>

<Header></Header>

{#each Data as data}

    <div>
        <p class="text-white">{data.markdown}</p>
    </div>

    <div class="w-11/12 md:w-1/2 bg-gray-900 bg-opacity-80 hiddenDiv rounded-xl my-3  mx-auto flex  flex-col shadow-xl justify-around " style="min-height:3rem;;overflow-x:auto;backdrop-filter:blur(4px);" >
        <div class="flex flex-row justify-between bg-black bg-opacity-10  py-1 px-1">
            <div class="py-1 px-3 opacity-80">
            </div>
            <button class="text-gray-200 tet-xl transform hover:bg-gray-600 hover:bg-opacity-50 hover:text-white py-1 px-3 rounded-lg transition-all duration-100 ease-in">copy 📄</button>
        </div>
        <div class="p-3">
            <pre class="whitespace-nowrap" style=""><code class="language-js text-base" >{data.code}</code></pre>
        </div>
    </div>
{/each}
    
<Footer></Footer>