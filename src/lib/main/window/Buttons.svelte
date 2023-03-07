<script>
  import Fa from "svelte-fa";
  import { faArrowLeftLong, faArrowRightLong } from "@fortawesome/free-solid-svg-icons"
  export let next;
  export let previous;
</script>

<div class="article-nav article-section">
  <button class="in-article-section" on:click={previous}>
    <div id="left-arrow">
      <Fa icon={faArrowLeftLong} size="3.5x" />
    </div> 
  </button>
  <button class="in-article-section" on:click={next}>
    <div id="right-arrow">
      <Fa icon={faArrowRightLong} size="3.5x" />
    </div>
  </button>
</div>

<style>
  * {
    cursor:none;
  }
  
  .article-nav {
    display: flex;
    min-height: 20px;
  }
  #right-arrow,
  #left-arrow {
    height: 100%;
    width: 100%;
    position: relative;
    display: flex;
    justify-content: center;
    flex-direction: column;
    transition: all 0.2s cubic-bezier(0,.69,.31,1.01);
    right: 0px;
  }
  #right-arrow:hover {
    right: -10px;
  }
  #right-arrow:active {
    right: -30px;
  }
  #left-arrow:hover {
    right: 10px;
  }
  #left-arrow:active {
    right: 30px;
  }

  .in-article-section {
    display: flex;
    background-color: transparent;
    border: 1px solid var(--border-color);
    justify-content: center;
    align-items: center;
    flex-basis: auto;
    flex-grow: 1;
    flex-shrink: 1;
  }
  .in-article-section:hover {
    border-color: #646cff;
  }
  .in-article-section:focus,
  .in-article-section:focus-visible {
    outline: 4px auto -webkit-focus-ring-color;
  }
</style>