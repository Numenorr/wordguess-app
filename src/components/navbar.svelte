<script>
  import Icon from "@iconify/svelte";
  import ModalTutorial from "./modalTutorial.svelte";
  let showModal = false;
</script>

<nav>
  <ul>
    <li><Icon icon="twemoji:books" /><strong>Que palavra é essa?</strong></li>
  </ul>
  <ul>
    <li>
      <a
        href="https://github.com/Numenorr/wordguess-app"
        target="_blank"
        rel="noreferrer">GitHub</a
      >
    </li>
    <li><a on:click={() => (showModal = true)}>Tutorial</a></li>
  </ul>
</nav>

<ModalTutorial bind:showModal>
  <h2 slot="header">Tente adivinhar a palavra secreta!</h2>

  <ol class="definition-list">
    <li>Use os significados retirados do Dicionario</li>
    <li>
      Use o botão <strong>Nova Palavra</strong> para mudar a palavra secreta
    </li>
    <li>Tente quantas vezes quiser!</li>
    <li>
      Você pode trocar a dica usando o botão acima do significado da palavra
      secreta
    </li>
    <li>Divirta-se!</li>
  </ol>

  Os significados foram retirados do
  <a
    href="https://www.dicio.com.br/"
    target="_blank"
    rel="noreferrer"
    style="margin-left: 2px;">Dicio</a
  >. API utilizada neste projeto:
  <a
    href="https://github.com/ThiagoNelsi/dicio-api"
    target="_blank"
    rel="noreferrer">dicio-api</a
  >
</ModalTutorial>
