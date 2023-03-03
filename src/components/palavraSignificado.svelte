<script>
  import Icon from "@iconify/svelte";
  export let word;
  export let wordDef;
  let loading = true;

  async function pesquisarPalavra() {
    wordDef = null;
    try {
      let res = await fetch("https://dicio-api-ten.vercel.app/v2/" + word);
      let data = await res.json();
      if (Array.isArray(data)) {
        wordDef = data[0];
      } else {
        wordDef = "No result";
      }
      loading = false;
    } catch (err) {
      loading = false;
    }
  }
</script>

<article>
  <button
    role="button"
    class="outline"
    data-tooltip="Mudar significado da palavra secreta"
    on:click={pesquisarPalavra}
  >
    <Icon
      icon="mdi:dice-multiple-outline"
      width="26"
      height="26"
    />
  </button>
  {#if wordDef !== null}
    <blockquote>
      {wordDef.meanings[Math.floor(Math.random() * wordDef.meanings.length)]}
      <footer>
        <cite>- Dicio</cite>
      </footer>
    </blockquote>
  {:else}
    <h1 aria-busy="true" />
  {/if}
</article>
