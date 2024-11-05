<script>
  export let assetPath;
  export let setView;
  export let content;
</script>

<main class="grid-menu">
  <nav>
    <ul>
      {#each content as bird}
        <li class="grid-menu-item">
          <a href="/"
            on:click={(e) => { e.preventDefault(); setView('detail', bird.slug, 1);}}>
            <img src="{assetPath}images/menu-pics/{bird.slug}-1.jpg" alt="">
            <h3>{bird.title}</h3>
          </a>
        </li>
      {/each}
    </ul>
  </nav>
</main>
