<script>
  import { fade } from "svelte/transition";
  import Buttons from "./window/Buttons.svelte"
  
  const eachPhoto = [
    { photo: "https://media.discordapp.net/attachments/1061320413373808741/1082722576314400858/yuyuko.jpg", 
      href: "https://konachan.com/post/show/353385/cherry_blossoms-cui_-jidanhaidaitang-fan-flowers-p", 
      desc: "Yuyuko in the cherry blossoms."
    },
    { photo: "https://media.discordapp.net/attachments/1061320413373808741/1082722568747896927/suwawako.jpg", 
      href: "https://konachan.com/post/show/353380/cui_-jidanhaidaitang-flowers-moriya_suwako-sleepin",
      desc: "Suwako for Corgi www", 
    },
    { photo: "https://media.discordapp.net/attachments/1061320413373808741/1082722567439274136/kogasa.jpg",
      href: "https://gelbooru.com/index.php?page=post&s=view&id=4566161",
      desc: "very cute umbrella girl"
    },
    { photo: "https://media.discordapp.net/attachments/1061320413373808741/1082722567934185522/mefrfr.jpg",
      href: "https://www.pixiv.net/en/artworks/104653730",
      desc: "Kimono."
    }
  ]
  let index = 0;
  const next = () => {
    index = (index + 1) % eachPhoto.length;
  }
  const previous = () => {
    if (index != 0) {
      index = (index - 1) % eachPhoto.length;
      return;
    }
    index = eachPhoto.length - 1;
  }
</script>

<main id="main-content">
  <!-- The different slides to navigate! -->
  <article>
      <div class="article-image-section article-section">
        {#each [eachPhoto[index]] as src (index)}
        <!-- extend images! -->
        <!-- https://stackoverflow.com/questions/66215735/extending-images-from-left-and-right-sides-of-text-to-edges-of-screen-while-main -->
          <div>
            <img transition:fade
              src={src.photo}
              alt=""
              class="cover"
              draggable="false"
              />
          </div>
        {/each}
      </div>
      <div class="article-description-section article-section">
        {#each [eachPhoto[index]] as src (index)}
          <p>
            <a transition:fade
              href={src.href}
              target="_blank" 
              rel="noopener noreferrer"
              >
              {src.desc}
            </a>
          </p>
        {/each}
      </div>
    <div class="article-info article-section">
      <img src="svelte.svg" alt="" style="padding: 1em;" draggable="false" />
      <p>Made with love with Svelte.</p>
      <p style="color: rgba(255, 255, 255, 0.5); font-size: x-small;">I just started 3 days ago so.. please pardon the bugs!</p>
      
    </div>
    <!-- Put Buttons.svelte here -->
    <Buttons next={next} previous={previous}/>
  </article>
</main>

<style>
  * {
    cursor:none;
  }

  .article-info {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
  }
  .article-description-section {
    display: flex;
    align-content: center;
    align-items: center;
    flex-direction: column;
    justify-content: flex-end;
    padding-bottom: 1em;
    padding-left: 2em;
    padding-right: 2em;
    mix-blend-mode: difference;
  }
  .article-description-section > p {
    position:absolute;
    text-align: center;
  }
  .article-image-section {
    display: flex;
    min-height: 40px;
    transform: translateZ(0);
  }
  .article-image-section > div {
    opacity: 0.75;
    background-color: transparent;
  }
  .cover {
    height: 100%;
    width: 100%;
    object-fit: cover;
    position: absolute;
  }


  main {
    height: 87vh;
    user-select: none;
    overflow: hidden;
  }
  main a {
    font-weight:900;
    font-size:large;
    color: var(--link-color);
    text-decoration: inherit;
    transition: all 0.2s ease-in;
    -webkit-user-drag: none; 
    letter-spacing: 1px;
  }
  main a:hover {
    color: var(--link-color-on-hover);
  }
  #main-content > article {
    display: grid;
    width: 100%;
    height: 100%;
    grid-template-columns: 2fr 1fr;
    grid-template-rows: 3fr 1fr;
  }
  #main-content .article-section {
    height: 100%;
    border: 1px solid var(--border-color);
  }
</style>