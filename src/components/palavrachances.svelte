<script>
  import Icon from "@iconify/svelte";
  export let acertou;
</script>

{#if acertou != false}
  <div>
    <span>
      <Icon
        icon="basil:check-outline"
        width="80"
        color="#16a34a"
      />
    </span>
    <p>Acertou</p>
  </div>
{:else}
  <div>
    <span>
      <Icon
        icon="basil:cross-outline"
        width="80"
        color="#e11d48"
      />
    </span>
    <p>Tente novamente</p>
  </div>
{/if}

<style>
  div {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-top: 1em;
    animation: ease-in 1s;
  }
</style>
