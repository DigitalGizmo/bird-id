<script>
  export let assetPath;
  export let detailSlug;
  export let imageIdx;
  export let setImageIdx;

  let audio = new Audio(assetPath + 'audio/' + detailSlug + '.mp3')

  function playSound() {
    audio.play();
  }
</script>

<main class="detail">
  <header>
    <h1>American Redstart</h1>
    <h2>Setophaga ruticilla {detailSlug} idx: {imageIdx}</h2>
  </header>

  <div class="full-view">
    <img src="{assetPath}images/full-pics/{detailSlug}-{imageIdx}.jpg"
    alt="bird name">
  </div>

  <div class="info">
    <article>
      <a href="/" on:click={(e) => { e.preventDefault(); playSound();}}>
        <img src="{assetPath}icons/forest.png"
        alt="bird song">
        Listen
      </a>      
      <p>American Redstarts are always on the move and almost seem hyperactive as they dash through trees after insects, rapidly spreading and closing their tails to startle and flush out possible prey.</p>
    </article>

    <section>
      <ul class="images">
        <li>
          <a href="/" on:click={(e) => { e.preventDefault(); setImageIdx(0);}}>
            <img src="{assetPath}images/menu-pics/{detailSlug}-0.jpg"
            alt="bird name">
          </a>
        </li>
        <li>
          <a href="/" on:click={(e) => { e.preventDefault(); setImageIdx(1);}}>
            <img src="{assetPath}images/menu-pics/{detailSlug}-1.jpg"
          alt="bird name">
            </a>
        </li>
        <li>
          <a href="/" on:click={(e) => { e.preventDefault(); setImageIdx(2);}}>
            <img src="{assetPath}images/menu-pics/{detailSlug}-2.jpg"
          alt="bird name">
          </a>
        </li>
      </ul>

      <dl class="facts">
        <dt>Order:</dt>
        <dd>Passeriformes</dd>
        <dt>Family:</dt>
        <dd>Parulidae</dd>
        <dt>Size:</dt>
        <dd> 4.3 - 5.1 in (11-13 cm)</dd>
        <dt>Range:</dt>
        <dd>Canada to South America; seen in Maine in summer</dd>
      </dl>

      <ul class="behavior">
        <li class="habitat">Forest</li>
        <li class="food">Insects</li>
        <li class="nest">Tree</li>
      </ul>
    </section>

  </div><!--/detail-info--->
</main>
