<script>
  export let detailContent;
  export let isModalShowing;
  export let setView;
  export let modalPosition;

</script>

  <div class="mini-pop"
    style="left: {modalPosition.x}px; top: {modalPosition.y}px; ">
    <p>{detailContent.title}</p>
    <p>
      <a href="/"
      on:click={(e) => { e.preventDefault(); setView('detail', detailContent.slug, 0);}}>
      Tap to learn about this bird
    </a>
    </p>
  </div>

<style>
  .mini-pop {
    /* top: 20px;
    left: 100px; */
    position: absolute;
    padding: 5px;
    width: 200px;
    height: 100px;
    background-color: yellow;
  }
</style>