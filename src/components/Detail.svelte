<script>
  export let assetPath;
  export let detailSlug;
  export let imageIdx;
  export let setImageIdx;
  export let content;
  export let playSound;

  let detailContent = content.find((element) => element.slug === detailSlug);
</script>

<main class="detail">
  <header>
    <h1>{detailContent.title}</h1>
    <h2>{detailContent.sciName}</h2>
  </header>

  <div class="full-view">
    <img src="{assetPath}images/full-pics/{detailSlug}-{imageIdx}.jpg"
    alt="{detailContent.title}">
  </div>

  <div class="info">
    <article>
      <ul class="images">
        <li>
          <a href="/" on:click={(e) => { e.preventDefault(); setImageIdx(0);}}>
            <img src="{assetPath}images/menu-pics/{detailSlug}-0.jpg"
            alt="{detailContent.title} thumbnail 1">
          </a>
        </li>
        <li>
          <a href="/" on:click={(e) => { e.preventDefault(); setImageIdx(1);}}>
            <img src="{assetPath}images/menu-pics/{detailSlug}-1.jpg"
          alt="{detailContent.title} thumbnail 2">
            </a>
        </li>
        <li>
          <a href="/" on:click={(e) => { e.preventDefault(); setImageIdx(2);}}>
            <img src="{assetPath}images/menu-pics/{detailSlug}-2.jpg"
          alt="{detailContent.title} thumbnail 3">
          </a>
        </li>
      </ul>

      <p>{detailContent.description}</p>
      <p class="credit">Bird songs, calls, and photographs courtesy of the Macaulay Library, Cornell Lab of Ornithology.</p>
    </article>

    <section>
      <div class="audio">
        <a href="/" on:click={(e) => { e.preventDefault(); playSound();}}>
          <img src="{assetPath}icons/audio-icon.png"
          alt="Play bird song">
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