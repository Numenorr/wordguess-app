<script>
  import Icon from "@iconify/svelte";
  import { afterUpdate } from "svelte";
  export let numLetras;
  export let letras = String;
  export let acertou = false;
  let char = [""];

  afterUpdate(() => {
    char = letras.split("");
    console.log(char + "  " + acertou);
  });
</script>

<div class="grid">
  {#if acertou === false}
    {#each Array(numLetras) as _, i}
      <div><Icon icon="carbon:dot-mark" /></div>
    {/each}
  {:else}
    {#each char as index, i}
      <div>{index}</div>
    {/each}
  {/if}
</div>

<style>
  div.grid {
    display: flex;
    justify-content: center;
  }

  div.grid > div {
    border: 1px solid;
    border-radius: 5px;
    padding: 0.9em;
  }
</style>
