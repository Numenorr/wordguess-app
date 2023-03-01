<script>
  import words from "../words.json";
  let word = words[1];
  let guess = "";
  let acertou = false;
  let loading = false;
  let wordDef = null;

  console.log(word);

  async function searchWord() {
    loading = true;
    wordDef = null;
    acertou = false;
    try {
      let res = await fetch(
        "https://api.dictionaryapi.dev/api/v2/entries/en/" + word
      );
      let data = await res.json();
      if (Array.isArray(data)) {
        wordDef = data[0];
        console.log(wordDef);
      } else {
        wordDef = "No result";
      }
      loading = false;
    } catch (err) {
      loading = false;
    }
  }

  function wordTest() {
    if (guess === word) {
      acertou = true;
      console.log("acertou");
    } else {
      console.log("tente dnv");
    }
  }
</script>

<button on:click={searchWord}> New word </button>

<form>
  {#if acertou === false}
    <input
      type="text"
      bind:value={guess}
      required
    />{:else}<input
      type="text"
      bind:value={guess}
      aria-invalid="false"
      required
    />{/if}

  <button
    on:click={wordTest}
    type="submit">test</button
  >
</form>
{#if wordDef !== null}
  <h1>
    {wordDef.meanings[0].definitions[Math.floor(Math.random() * 6)].definition}
  </h1>
{:else}
  <h1 aria-busy="true" />
{/if}
