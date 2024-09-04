<script>
  import Grid from './components/Grid.svelte'
  import Photo from './components/Photo.svelte'
  import Detail from './components/Detail.svelte'
  import Counter from './lib/Counter.svelte'

  let view = 'photo';
  let detailSlug = 'americanredstart';

  function setView(_view, _slug = 'bluejay') {
    detailSlug = _slug;
    view = _view;
  }

</script>

<header class="top">
  <h1>Bird I.D.</h1>
  <h2>Tap a bird to learn more</h2>

  <div class="view-sort">
    <p>View:
    <a href="/" on:click={(e) => { e.preventDefault(); setView('photo');}}>
      Photo</a> | 
    <a href="/" on:click={(e) => { e.preventDefault(); setView('grid');}}>
    Grid </a>
  </p>
  {#if view === 'grid'}
    <p>Sort by: Name | Size | Color</p>
  {/if}
  </div>
</header>
{#if view === 'grid'}
  <Grid 
    setView = {setView}
  />
{:else if view === 'photo'}
  <Photo />
{:else if view === 'detail'}
  <Detail 
    detailSlug = {detailSlug}
  />
{/if}


