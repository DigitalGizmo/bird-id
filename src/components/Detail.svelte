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
      <a href="/" on:click={(e) => { e.preventDefault(); playSound();}}>
        <img class="audio" src="{assetPath}icons/audio-icon.png"
        alt="bird song">
        Listen
      </a>      
      <p>{detailContent.description}</p>
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
      <ul class="behavior">
        <li class="habitat">Forest</li>
        <li class="food">Insects</li>
        <li class="nest">Tree</li>
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

    </section>

  </div><!--/detail-info--->
</main>

<style>
  .audio {
    width: 60px;
  }
</style>
