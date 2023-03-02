<script>
  import words from "../words.json";
  import Icon from "@iconify/svelte";
  import PalavraSecreta from "../components/palavraSecreta.svelte";

  let word = words[Math.floor(Math.random() * 21)];
  let guess = "";
  let acertou = false;
  let loading = false;
  let wordDef = null;
  let chances = 0;

  console.log(word);

  async function pesquisarPalavra() {
    loading = true;
    wordDef = null;
    acertou = false;
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

  async function novaPalavra() {
    word = words[Math.floor(Math.random() * 28)];
    chances = 0;
    acertou = false;
    try {
      let res = await fetch("https://dicio-api-ten.vercel.app/v2/" + word);
      let data = await res.json();
      if (Array.isArray(data)) {
        wordDef = data[0];
      } else {
        wordDef = "No result";
      }
    } catch (err) {
      loading = false;
    }
  }

  function adivinhar() {
    if (chances <= 5)
      if (guess === word) {
        acertou = true;
        console.log("acertou");
      } else {
        chances++;
        console.log("tente dnv" + chances);
      }
    else console.log("acabou");
  }
</script>

<article>
  <button on:click={novaPalavra}>Nova palavra</button>
  <PalavraSecreta
    numLetras={word.length}
    letras={word}
    {acertou}
  />
</article>
<form>
  {#if acertou === false}
    <input
      type="text"
      bind:value={guess}
      required
    />
  {:else}
    <input
      type="text"
      bind:value={guess}
      aria-invalid="false"
      required
    />
  {/if}

  <button
    on:click={adivinhar}
    type="submit">Adivinhar</button
  >
</form>
<Icon icon="basil:check-outline" />
<Icon icon="basil:cross-outline" />
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
    </blockquote>
  {:else}
    <h1 aria-busy="true" />
  {/if}
</article>

<section>
  Descrições retiradas de
  <a href="https://www.dicio.com.br/">Dicio</a>.
</section>
