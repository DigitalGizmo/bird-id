<script>
  import Grid from './components/Grid.svelte'
  import Photo from './components/Photo.svelte'
  import Detail from './components/Detail.svelte'
  import content from './lib/content.json'

  let view = 'photo';
  let detailSlug = 'americanredstart';
  let imageIdx = 0;

  const assetPath = "https://assets.digitalgizmo.com/bird-id/";
  // const assetPath = "";

  function setView(_view, _slug = 'bluejay', _imageIdx = 0) {
    detailSlug = _slug;
    setImageIdx(_imageIdx);
    view = _view;
  }

  function setImageIdx(_idx) {
    imageIdx = _idx;
    // console.log(' setting idx to: ' + imageIdx);
  }

</script>

<header class="top">
  <div class="title">
    <h1>Bird I.D.</h1>
    <h2>Tap a bird to learn more</h2>
  </div>
  
  <div class="view-sort">
    <p>Menu View</p>

    <a href="/" on:click={(e) => { e.preventDefault(); setView('photo');}}>
      <img src="{assetPath}icons/photo-icon.png" alt="photo menu icon">
    </a>
    <a href="/" on:click={(e) => { e.preventDefault(); setView('grid');}}>
      <img src="{assetPath}icons/grid-icon.png" alt="grid menu icon">
    </a>
  {#if view === 'grid'}
    <p>Sort by: Name | Size | Color</p>
  {/if}
  </div>
</header>
{#if view === 'grid'}
  <Grid 
    assetPath = {assetPath}
    setView = {setView}
    content = {content}
  />
{:else if view === 'photo'}
  <Photo 
    assetPath = {assetPath}
    setView = {setView}
    content = {content}
  />
{:else if view === 'detail'}
  <Detail 
    assetPath = {assetPath}
    detailSlug = {detailSlug}
    imageIdx = {imageIdx}
    setImageIdx = {setImageIdx}
    content = {content}
  />
{/if}


