<script>
  export let detailContent;
  export let isModalShowing;
  export let setView;
  export let modalPosition;

</script>

  <div class="mini-pop"
    style="left: {modalPosition.x}px; top: {modalPosition.y}px; ">
    <h3>{detailContent.title}</h3>
    <p>
      <a href="/"
      on:click={(e) => { e.preventDefault(); setView('detail', detailContent.slug, 0);}}>
      Tap to learn about this bird
    </a>
    </p>
  </div>