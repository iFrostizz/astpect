<script lang="ts">
import { invoke } from '@tauri-apps/api/tauri'
import { onMount } from 'svelte';

let name = ''
let greetMsg = ''

async function greet() {
  greetMsg = await invoke('greet', { name })
};

onMount(() => {
let input = document.getElementById("file-input");

input?.addEventListener("change", function() {
    console.log("file changed");
    let files = input.files;

    let file = files[0];
    let reader = new FileReader();
    reader.onload = function() {
      let content = reader.result;
      console.log(content);
      }
      reader.readAsText(file);
    });

});
</script>

<div>
<input id="greet-input" placeholder="Enter a name..." bind:value="{name}" />
<button on:click="{greet}">Greet</button>
<p>{greetMsg}</p>
<!-- <button id="file-input"> -->
<input type="file" id="file-input" multiple>
<!-- </button> -->
</div>
