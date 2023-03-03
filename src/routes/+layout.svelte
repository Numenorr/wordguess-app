<script>
  import "@picocss/pico";
  import Navbar from "../components/navbar.svelte";
</script>

<main class="container">
  <Navbar />
  <slot />
  <footer>Feito por <a href="sds">Filipe Cardoso</a></footer>
</main>
