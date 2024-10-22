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

      <!-- place holders -->
      <li class="grid-menu-item">
        <a href="/">
          <img src="{assetPath}images/menu-pics/bobolink.jpg" alt="">
          <h3>Bobolink</h3>
        </a>
      </li>
      <li class="grid-menu-item">
        <a href="/">
          <img src="{assetPath}images/menu-pics/blackcappedchickadee.jpg" alt="">
          <h3>Black-capped Chickadee</h3>
        </a>
      </li>
      <li class="grid-menu-item">
        <a href="/">
          <img src="{assetPath}images/menu-pics/barnowl.jpg" alt="">
          <h3>Barn Owl</h3>
        </a>
      </li>
      <li class="grid-menu-item">
        <a href="/">
          <img src="{assetPath}images/menu-pics/americanredstart.jpg" alt="">
          <h3>American Redstart</h3>
        </a>
      </li>
      <li class="grid-menu-item">
        <a href="/">
          <img src="{assetPath}images/menu-pics/crow.jpg" alt="">
          <h3>Crow</h3>
        </a>
      </li>
      <li class="grid-menu-item">
        <a href="/">
          <img src="{assetPath}images/menu-pics/burrowingowl.jpg" alt="">
          <h3>Burrowing Owl</h3>
        </a>
      </li>
      <li class="grid-menu-item">
        <a href="/">
          <img src="{assetPath}images/menu-pics/bluejay.jpg" alt="">
          <h3>Blue Jay</h3>
        </a>
      </li>
      <li class="grid-menu-item">
        <a href="/">
          <img src="{assetPath}images/menu-pics/bobolink.jpg" alt="">
          <h3>Bobolink</h3>
        </a>
      </li>
    </ul>
  </nav>
</main>
