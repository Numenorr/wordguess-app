<script>
  import words from "../words.json";
  import Icon from "@iconify/svelte";
  import PalavraSecreta from "../components/palavraSecreta.svelte";
  import PalavraSignificado from "../components/palavraSignificado.svelte";
  import Palavrachances from "../components/palavrachances.svelte";

  let palavra = words[Math.floor(Math.random() * 18)];
  let guess = "";
  let acertou = false;
  let loading = false;
  let wordDef = null;
  let chances = 0;

  console.log(palavra);

  async function novaPalavra() {
    palavra = words[Math.floor(Math.random() * 18)];
    chances = 0;
    acertou = false;
    try {
      let res = await fetch("https://dicio-api-ten.vercel.app/v2/" + palavra);
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
      if (guess.toLowerCase() === palavra) {
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
    numLetras={palavra.length}
    letras={palavra}
    {acertou}
  />
  {#if chances > 0}
    <Palavrachances {acertou} />
  {/if}
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

<PalavraSignificado
  word={palavra}
  {wordDef}
/>
