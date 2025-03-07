<script>
  import { onMount } from 'svelte';
  import Grid from './components/Grid.svelte'
  import Photo from './components/Photo.svelte'
  import Detail from './components/Detail.svelte'
  import content from './lib/content.json'

  let view = 'photo';
  let currMenuView = "photo";
  let detailSlug = 'americanredstart';
  let imageIdx = 0;
  let sortOrder = 'alphabetical'; // Default to alphabetical sorting

  const assetPath = "https://assets.digitalgizmo.com/bird-id/";
  // const assetPath = "";

  // Update setView function to reset the timer whenever the view changes
  function setView(_view, _slug = 'bluejay', _imageIdx = 0) {
    detailSlug = _slug;
    setImageIdx(_imageIdx);
    view = _view;
    if (view != "detail") {
      currMenuView = view;
    }
    
    // Reset the inactivity timer when the view changes
    resetInactivityTimer();
  }


  function setImageIdx(_idx) {
    imageIdx = _idx;
    // console.log(' setting idx to: ' + imageIdx);
  }
  
  // New function to handle sorting
  function setSortOrder(_sortOrder) {
    sortOrder = _sortOrder;
  }

  /* ---- Timeout code ----*/
  let timeoutDuration = 60000; // 120000 2 minutes (in milliseconds)
  let inactivityTimer;

  function resetInactivityTimer() {
    // Clear any existing timer
    clearTimeout(inactivityTimer);
    
    // Only set the timer if we're not already on the photo view
    if (view !== 'photo') {
      inactivityTimer = setTimeout(() => {
        // Always return to the photo view
        setView('photo');
      }, timeoutDuration);
    }
  }


  // Need to track user activity to reset the timer
  function setupActivityTracking() {
    // These are common user interaction events
    const events = ['mousedown', 'mousemove', 'keypress', 'scroll', 'touchstart'];
    
    // Add event listeners for each type of user activity
    events.forEach(event => {
      window.addEventListener(event, resetInactivityTimer, true);
    });
    
    // Initialize the timer
    resetInactivityTimer();
  }

  onMount(() => {
    setupActivityTracking();
    
    // Clean up event listeners when component is destroyed
    return () => {
      const events = ['mousedown', 'mousemove', 'keypress', 'scroll', 'touchstart'];
      events.forEach(event => {
        window.removeEventListener(event, resetInactivityTimer, true);
      });
      clearTimeout(inactivityTimer);
    };
  });

</script>

<header class="top">
  <div class="title">
    <h1>Bird I.D.</h1>
    {#if view === 'detail'}
      <h2>
        <a href="/" on:click={(e) => { e.preventDefault(); setView(currMenuView);}}>
          &larr; Return to menu
        </a>
      </h2>
    {:else}
      <h2>Tap a bird to learn more
      {#if view === 'grid'}
        &nbsp;&nbsp;...&nbsp;&nbsp;Scroll to show more
      {/if}
    </h2>
    {/if}
  </div>
  
  <div class="view-sort">
    <p class="menu">Menu View:</p>

    <a href="/" on:click={(e) => { e.preventDefault(); setView('photo');}}>
      <img src="{assetPath}icons/photo-icon{currMenuView === 'photo' ? '-selected' : ''}.png" 
      alt="bird display menu icon">
    </a>
    <a href="/" on:click={(e) => { e.preventDefault(); setView('grid');}}>
      <img src="{assetPath}icons/grid-icon{currMenuView === 'grid' ? '-selected' : ''}.png" 
      alt="grid menu icon">
    </a>
  {#if view === 'grid'}
    <p>Sort by: 
      <a href="/" class={sortOrder === 'alphabetical' ? 'active-sort' : ''} on:click={(e) => { e.preventDefault(); setSortOrder('alphabetical');}}>Name</a> | 
      <a href="/" class={sortOrder === 'size' ? 'active-sort' : ''} on:click={(e) => { e.preventDefault(); setSortOrder('size');}}>Size ↑</a> | 
      <a href="/" class={sortOrder === 'size-desc' ? 'active-sort' : ''} on:click={(e) => { e.preventDefault(); setSortOrder('size-desc');}}>Size ↓</a> | 
      <a href="/" class={sortOrder === 'color' ? 'active-sort' : ''} on:click={(e) => { e.preventDefault(); setSortOrder('color');}}>Color</a>
    </p>
  {/if}
  </div>
</header>
{#if view === 'grid'}
  <Grid 
    assetPath = {assetPath}
    setView = {setView}
    content = {content}
    sortOrder = {sortOrder}
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

<style>
  .active-sort {
    color: #FFB802;
    font-weight: bold;
  }
</style>