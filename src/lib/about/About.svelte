<script>
  import { Parallax, ParallaxLayer } from "svelte-parallax";
  import { link } from "svelte-routing";
    import { onMount } from "svelte";
  const qa = [
    {question: "Who are you?", answer: "I'm Lilyn/Alice! An osu player.."},
    {question: "What's your real name?" , answer: "Who shares their real name in the internet?"},
    {question: "Can you do websites for me?", answer: "I mean.. sure but don't expect a good product."},
    {question: "Career?", answer: "osu!.. and probably software development."},
    {question: "Favorite food?", answer: "Sisig."}
  ]
  const videos = [
    "https://cdn.discordapp.com/attachments/1061320413373808741/1082662181016965200/felis-wtf.mp4",
    "https://cdn.discordapp.com/attachments/988083238977294447/1081549996199006359/remap.mp4",
    "https://cdn.discordapp.com/attachments/988083238977294447/1075485694622978190/thehell.mp4",
    "https://cdn.discordapp.com/attachments/988083238977294447/1068916741226377216/myaimgotmoreflowy.mp4",
  ]

  let parallax;

  let enableParallax = true;
  onMount(() => {
    enableParallax = false;
    const play_section = document.querySelector("div#osu-play-section")
    const videos = play_section.querySelectorAll("video");
    videos.forEach(function(video) {
      video.addEventListener("mouseover", function() {
        video.volume = 0.02
        video.play();
      });
      video.addEventListener("mouseleave", function() {
        video.pause();
      });
    });
  })

  const scrolls = [1.9, 2.95]
  let index = 0;
  const next = () => {
    index = (index + 1) % scrolls.length;
  }
</script>

<div id="about-page">
  <div id="floating-menu">
    <img 
      src="https://media.discordapp.net/attachments/1064502678195032174/1081625254989942874/18682614.jpg" 
      alt="" 
      class="creator-picture"
      draggable="false"
    />
    <a href="/" use:link id="floating-button">
      Back
    </a>
    {#each [scrolls[index]] as scroll (index)}
      <button 
        on:click={() => {
          parallax.scrollTo(scroll, { duration: 1000 })
          next()
        }}
      >
        Scroll
      </button>
    {/each}
  </div>

  <div id="parallax-section">
    <Parallax 
      sections={4} 
      bind:this={parallax}
      config={{ stiffness: 0.08, damping: 0.5 }}
      disabled={enableParallax}
    >
      <ParallaxLayer
        offset={0}
        rate={0.5}
        style="
          display: flex;
          background-color:transparent;
        "
      >
        <img src="space-boy.png" alt=""/>
      </ParallaxLayer>

      {#each qa as { question, answer }, index}
        <ParallaxLayer
          offset={1 + index/8}
          rate={0.3 + index/4}
          style="
            display:flex;
            justify-content:space-around
          "
        >
          <div>
            <div class="question">
              <h2 >{question}</h2>
            </div>
          </div>
          <div>
            <div class="answer">
              <p >{answer}</p>
            </div>
          </div>
        </ParallaxLayer>
      {/each}

      <ParallaxLayer
        offset={2}
        rate={1.8}
        style="
          display:flex;
          justify-content:space-evenly;
          z-index:-2;
        "
      >
      <div>
        <h1 style="background-color:black">osu! plays!</h1>
      </div>
        
      </ParallaxLayer>

      <ParallaxLayer
        offset={2}
        rate={1}
        style="
          display:flex;
          justify-content:space-evenly;
          align-items:center;
        "
      >
        <!-- svelte-ignore a11y-media-has-caption -->
        <div class="example-grid" id="osu-play-section">
          {#each videos as video}
              <video 
                src={video}
                loop
                width="500"
                class="video-section"
              />
          {/each}
        </div>
      </ParallaxLayer>
      

      <div id="start-parallax">
        <ParallaxLayer 
          offset={0} 
          rate={1.3} 
          style="
            background-color:rgba(0, 0, 0, 0.4);
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;
          "
        >
          <h1>Welcome to the about page!</h1>
          <p>You're actually reading this part.</p>
          <p style="color:rgba(255, 255, 255, 0.2)">Page reload or resize is needed for the library to work for some reason.. Please reload the page!</p>
        </ParallaxLayer>
      </div>
    </Parallax>
  </div>
</div>

<style>
  .question {
    background-color: rgba(0, 0, 0, 0.5);
    padding: 2em;
    transition: background-color 0.2s ease;
  }
  .question:hover {
    background-color: rgba(0, 0, 0, 1);
  }
  .answer {
    background-color: rgba(255, 255, 255, 0.8);
    padding: 2em;
    margin-top:2em;
    color:black;
    transition: background-color 0.2s ease;
  }
  .answer:hover {
    background-color: rgba(255, 255, 255, 1);
  }

  .example-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: 1fr 1fr;
    column-gap: -10px;
    gap: 10px;
  }

  .video-section {
    border: 1px solid var(--border-color);
    background-color: rgba(0, 0, 0, 0.5);
    opacity: 0.5;
    transition: opacity 0.2s ease;
  }
  .video-section:hover {
    opacity: 1;
  }

  #about-page {
    height: 100%;
    width: 100%;
    pointer-events: all;
    cursor:default;
  }
  img {
    height: 50%;
    width: 100%;
    object-fit: cover;
  }
  .creator-picture {
    max-width: 20%;
    height: auto;
    border-radius: 50%;
  }
  a {
    border: 1px solid transparent;
    padding: 1em 3em;
    background-color: rgba(0, 0, 0, 0.5);
    border-radius: 10%;
    transition: scale 0.1s ease, border-color 0.2s ease-out;
    scale: 1;
    text-decoration: none;
    color: var(--text-color);
  }
  a:hover {
    scale: 1.1;
    border-color: #646cff;
  }
  #floating-menu {
    display: flex;
    gap: 2em;
    align-items: center;
    position: fixed;
    z-index: 1000;
    user-select: none;
    margin: 2em;
  }
  button {
    padding: 1.5em 3.5em;
    border-radius: 10%;
    background-color: rgba(0, 0, 0, 0.5);
    transition: scale 0.1s ease;
    scale: 1;
    color: var(--text-color);
  }
  button:hover {
    scale: 1.1;
    border-color: #646cff;
  }
</style>