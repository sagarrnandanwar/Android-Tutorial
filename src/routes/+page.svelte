<script>
  
     import './prism-dark.css'
     import {Data} from "../lib/data"
   
</script>
 

{#each Data as data}
    <div class="w-11/12 md:w-1/2 bg-gray-900 hiddenDiv rounded-xl my-3  mx-auto flex gap-2 flex-col shadow-xl justify-around " style="min-height:3rem;;overflow-x:auto" >
        <div class="flex flex-row justify-between bg-gradient-to-b from-black  py-1 px-1">
            <div class="py-1 px-3 opacity-80">
                
            </div>
            <button class="text-gray-200 tet-xl transform hover:bg-gray-700 hover:text-white py-1 px-3 rounded-lg">copy 📄</button>
        </div>
        <div class="p-3">
            <pre class="whitespace-nowrap" style=""><code class="language-js text-base" >{data.code}</code></pre>
        </div>
    </div>
{/each}
    