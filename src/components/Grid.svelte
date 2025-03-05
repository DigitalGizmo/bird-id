<script>
  export let assetPath;
  export let setView;
  export let content;
  export let sortOrder = 'alphabetical'; // Default to alphabetical sorting
  
  // Function to sort content based on sortOrder
  $: sortedContent = [...content].sort((a, b) => {
    if (sortOrder === 'alphabetical') {
      return a.title.localeCompare(b.title);
    } else if (sortOrder === 'size') {
      // Sort by size from smallest to largest
      return parseInt(a.sizeOrdinal) - parseInt(b.sizeOrdinal);
    } else if (sortOrder === 'size-desc') {
      // Sort by size from largest to smallest
      return parseInt(b.sizeOrdinal) - parseInt(a.sizeOrdinal);
    } else if (sortOrder === 'color') {
      return parseInt(a.colorCode) - parseInt(b.colorCode);
    }
    return 0;
  });
</script>

<main class="grid-menu">
  <nav>
    <ul>
      {#each sortedContent as bird}
        <li class="grid-menu-item">
          <a href="/"
            on:click={(e) => { e.preventDefault(); setView('detail', bird.slug, 1);}}>
            <img src="{assetPath}images/menu-pics/{bird.slug}-1.jpg" alt="{bird.title}">
            <h3>
              {bird.title}
              {#if sortOrder === 'size' || sortOrder === 'size-desc'}
                <span class="size-info">{bird.sizeDescription}</span>
              {/if}
            </h3>
          </a>
        </li>
      {/each}
    </ul>
  </nav>
</main>

<style>
  .size-info {
    display: block;
    font-size: 0.8em;
    font-weight: normal;
    opacity: 0.8;
  }
</style>