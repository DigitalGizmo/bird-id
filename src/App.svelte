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
  let audio = null; // Audio instance

  const assetPath = "https://assets.digitalgizmo.com/bird-id/";
  // const assetPath = "";

  // Function to play audio
  function playSound() {
    // Create a new audio instance each time to avoid state issues
    audio = new Audio(assetPath + 'audio/' + detailSlug + '.mp3');
      
    // Add event listeners to track when audio ends
    audio.addEventListener('ended', () => {
      audio.currentTime = 0;
    });
      
    // Set volume and play
    audio.volume = 1.0;
      
    // Use a promise to handle play() since it returns a promise on modern browsers
    const playPromise = audio.play();
      
    // Handle potential play() promise rejection (common in iOS)
    if (playPromise !== undefined) {
      playPromise.catch(error => {
        console.log("Audio play failed:", error);
      });
    }
  }

  // Function to stop audio - more compatible approach
  function stopSound(immediate = false) {
    if (audio && !audio.paused) {
      if (immediate) {
        // Force immediate stop - more reliable on iOS
        audio.pause();
        audio.currentTime = 0;
        return;
      }
      
      try {
        // Simple approach that should work on iOS
        // Instead of trying to fade out (which can be problematic on iOS),
        // we'll just pause after a short delay to give a sense of completion
        setTimeout(() => {
          audio.pause();
          audio.currentTime = 0;
        }, 300);
      } catch (e) {
        // Fallback if the above fails
        console.log("Error stopping audio:", e);
        audio.pause();
        audio.currentTime = 0;
      }
    }
  }

  // Update setView function to reset the timer whenever the view changes
  function setView(_view, _slug = 'bluejay', _imageIdx = 0) {
    // Stop any playing audio when changing views
    stopSound(true);
    
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
  let timeoutDuration = 120000; // 60000 = 1 minute (in milliseconds)
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
      stopSound(true); // Force immediate audio stop when component is destroyed
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
         ... Scroll for more
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
    playSound = {playSound}
  />
{/if}

<style>
  .active-sort {
    color: #FFB802;
    font-weight: bold;
  }
</style>