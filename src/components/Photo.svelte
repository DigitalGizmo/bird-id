<script>
  import { onMount } from 'svelte';
  import LabelModal from "./LabelModal.svelte";
  export let assetPath;
  export let setView;
  export let content;

  let photoHeight = 1366;
  let photoWidth = 1024;
  // let modalLeft = 200;
  // let modalTop = 100;
  let modalPosition = {"x": 200, "y": 100};
  let svgHtmlRatio = 1;
  // let svgHtmlYRatio = 1;

  let isModalShowing = false;
  // let birdTitle = "tbd";
  let detailContent;

  onMount(() => {
    let exploded = document.getElementById('photo');
    let rect = exploded.getBoundingClientRect();
    // photoWidth =  Math.round(rect.width);
    photoHeight =  Math.round(rect.height);
    svgHtmlRatio = photoHeight/1366;
    console.log('default modalPosition x: ' + modalPosition.x);
  })


  function showLabel(_slug) { 
    detailContent = content.find((element) => element.slug === _slug);
    modalPosition.x = (detailContent.labelPos.x * svgHtmlRatio)-200;
    modalPosition.y = (detailContent.labelPos.y * svgHtmlRatio)-100;

    console.log('modalPosition x in show: ' + modalPosition.x);

    isModalShowing = true;
  };  
</script>

<main class="photo-menu">
  <div>
    <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" 
      viewBox="0 0 1024 1366">
    
      <g id="photo">
        <image width="1024" height="1366" 
        href="{assetPath}images/menu-pics/bird-case-exploded.jpg"/>
      </g>
    
      <g id="hotspots">
        <a href="/"
          on:click={(e) => { e.preventDefault(); showLabel('common-raven');}}>
          <path id="raven" class="hotspot" d="m339.02,459.98c6.04-8.84,21.88-7.68,26.61-7.68,3.54-2.96,18.41-8.4,25.5,3.12,7.09,11.52,13,31.6,16.54,33.38,3.54,1.77,7.83,3.99,8.27,7.68,7.97-4.58,36.18,40.54,38.99,47.26,1.84,4.39,14.64,34.98,11.69,34.39-2.95-.59-18.77-30.26-17.59-23.76,1.18,6.5,6.62,7.64,3.31,14.18,5.17.89,7.91,9.96,6.73,9.95-1.18,0-4.73-2.27-3.54,2.46,1.18,4.73,16.69,23.92,9.45,31.59-2.76,2.92-2.44.3-7.16.9-2.88,6.05,0,0-19.78-.95-9.9-11.6-9.52-17.91-7.98-24.25,2.51-10.39-2.77-12.95-6.5-12.88-14.41.27-4.06,16-21.56,9.36-4.1-1.56,9.3-12.85,18.39-12.63l-1.77-6.2c-13.73-1.99-2.88,11.3-19.24,10.19-2.24,11.3-11.94,8.77-12.88,7.31-1.88-2.94,2.44-10.41,13.96-11.3,2.05-3.05.86-7.61.21-11.45-1.59-9.3-19.79-22.8-25.69-31.99-9.07-14.15-5.88-34.11-4.75-44.57-.59-5.32-3.17-12.3-8.01-16.38-6.5-5.47-23.17-7.71-23.17-7.71Z"/>
        </a>
    
        <a href="/"
          on:click={(e) => { e.preventDefault(); showLabel('pileated-woodpecker');}}>
          <path id="pileated" class="hotspot" d="m625.95,640.31c-.89,6.69,11.13,12.87,9.65,17.3s1.15,8.57-5.45,7.97-21.93-11.46-29.02-12.97-38.95-1.75-69.11,23.73c-10.49,8.86,7.88,28.06,21.47,22.06,8.68-3.83,21.06,14.56,42.62,12.6,13.77-1.26,30.58,6.69,33.53-3.65,8.57.89-.29,19.79-2.35,28.35s9.88,31.01,15.19,30.13,19.93-22.93,16.98-30.32-6.14-11.07-4.22-19.02c2.07-8.53,3.71-11.95,7.07-12.1,3.8,4.14,5.86,11.22,26.24,3.35,6.28-2.43,10.63,1.97,31.6-13.1,16.84,1.18,44.6-11.66,29.11-28.71s-41.88-17.13-55.46-16.24-22.61,5.05-29.47,10.11c-8.42,6.2-20.12-1.4-18.05-7.61s11.58-16.41,17.53-19.63c-.95-1.41-9.81-3.46-13.65-.36,0,0-4.17-.38-7.42-1.49s-16.21,5.16-16.8,9.59Z"/>
        </a>
    
        <a href="/"
          on:click={(e) => { e.preventDefault(); showLabel('blackburnian-warbler');}}>
          <path id="warbler" class="hotspot" d="m349.05,1259.24c6.54-5.47,16.4,1.6,24.37,2.22,4.78.37,9.3,3.54,6.65,3.54,0,0-10.63,3.99-11.96,7.53s-4.43,9.41-7.09,10.74-15.95-.75-11.96-2.52,5.57-3.88,5.57-3.88c-7.97-.44-11.33-6.33-8.67-9.66,2.16-2.7-.61-4.87,3.1-7.97Z"/>
        </a>
        
        <a href="/"
          on:click={(e) => { e.preventDefault(); showLabel('barn-owl');}}>
          <path class="hotspot" d="m524.96,395.39c-12.41,7.09-31.12,30.82-24.92,33.92,12.9,6.45,20.66,6.64,31.98,5.43,3.64-.39,4.43,1.69,5.32,4.87s-6.71,12.65.94,14.6c5.43,1.38,12.57,2.78,14.12-3.96,1.33-5.76-14.62-11.08-7.97-14.62,3.5-1.86,7.17-4.89,8.86-2.66,9.75,12.85,9.22,21.96,9.22,21.96,0,0,3.52,14.65,10.27,6.4,3.99-4.87-7.53-15.51-8.64-21.27-2.05-10.67-1.11-30.13-1.11-30.13,7.97-6.2,17.83-18.86,14.77-27.27,31.75,12.65,45.48-12.13,63.56-38.3s105.39-47.67,54.58-70.44c-25.7-11.52-85.06,16.39-88.61,21.71s-27.03,27.91-27.47,45.38c-8.86-10.63-13.25-9.05-22.15-9.05-11.96,0-17.59,16.34-14.18,19.16,5.76,4.76,19.3-.17,22.84,6.92s3.02,16.45-.53,16.45-2.82-11.96-10.8-6.42c-3.25,2.26,7.82,17.21,5.32,19.71-3.1,3.1-17.28,1.33-26.58-4.87,0,7.97-6.2,7.53,1.41,19.74-8.3-3.25-10.25-7.25-10.25-7.25Z"/>
        </a>
      </g>
    </svg>
  </div>


  {#if isModalShowing}
    <LabelModal 
      modalPosition = {modalPosition}
      detailContent = {detailContent}
      setView = {setView}
    />
  {/if}  

</main>

<style>
  .photo-menu{
    position: relative;
  }
</style>