<script>
  export let assetPath;
  export let detailSlug;
  export let imageIdx;
  export let setImageIdx;
  export let content;

  let audio = new Audio(assetPath + 'audio/' + detailSlug + '.mp3')
  let detailContent = content.find((element) => element.slug === detailSlug);

  function playSound() {
    audio.play();
  }
</script>

<main class="detail">
  <header>
    <h1>{detailContent.title}</h1>
    <h2>{detailContent.sciName}</h2>
  </header>

  <div class="full-view">
    <img src="{assetPath}images/full-pics/{detailSlug}-{imageIdx}.jpg"
    alt="bird name">
  </div>

  <div class="info">
    <article>
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
<!--         <li> hi Don, we said we'd have up to four thumbs, didn't we?
          <a href="/" on:click={(e) => { e.preventDefault(); setImageIdx(3);}}>
            <img src="{assetPath}images/menu-pics/{detailSlug}-3.jpg"
          alt="bird name">
          </a>
        </li> -->
      </ul>

      <p>{detailContent.description}</p>
      <p class="credit">Bird songs, calls, and photographs courtesy of the Macaulay Library, Cornell Lab of Ornithology.</p>
    </article>

    <section>
      <div class="audio">
        <a href="/" on:click={(e) => { e.preventDefault(); playSound();}}>
          <img src="{assetPath}icons/audio-icon.png"
          alt="bird song">
          <span class="">Listen</span>
        </a>
      </div>

      <ul class="behavior">
        <li class="habitat">{detailContent.habitat}</li>
        <li class="food">{detailContent.food}</li>
        <li class="nest">{detailContent.nest}</li>
      </ul>

      <dl class="facts">
        <dt>Order:</dt>
        <dd>{detailContent.order}</dd>
        <dt>Family:</dt>
        <dd>{detailContent.family}</dd>
        <dt>Size:</dt>
        <dd>{detailContent.sizeDescription}</dd>
        <dt>Range:</dt>
        <dd>{detailContent.range}</dd>
      </dl>

    </section>

  </div><!--/detail-info--->
</main>
