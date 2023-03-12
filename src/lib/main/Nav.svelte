<script>
  import Fa from "svelte-fa";
  import { faCakeCandles } from "@fortawesome/free-solid-svg-icons";
  import {
    faTwitter,
    faDiscord,
    faTwitch,
    faGithub,
  } from "@fortawesome/free-brands-svg-icons";

  import { link } from "svelte-routing";
</script>

<!-- svelte-ignore a11y-invalid-attribute -->
<nav id="nav-menu">
  <div id="nav-logo-section" class="nav-section">
    <a href="#" target="_blank" rel="noopener noreferrer" draggable="false">
      <Fa icon={faCakeCandles} size="2.5x" />
    </a>
    <h2>Alice's Website</h2>
  </div>
  <div id="nav-link-section" class="nav-section">
    <a href="/lilys-website/about" use:link draggable="false">ABOUT</a>
    <a href="#" draggable="false">PROJECTS</a>
  </div>
  <div id="nav-social-section" class="nav-section">
    <a href="https://twitter.com/LilynHana" target="_blank" rel="noopener noreferrer" draggable="false">
      <!-- Transition it to make it larger -->
      <Fa icon={faTwitter} />
    </a>
    <a href="https://discord.gg/myDk44yk6J" target="_blank" rel="noopener noreferrer" draggable="false">
      <Fa icon={faDiscord} />
    </a>
    <a href="https://www.twitch.tv/lilyn_h" target="_blank" rel="noopener noreferrer" draggable="false">
      <Fa icon={faTwitch} />
    </a>
    <a href="https://github.com/DoormatIka" target="_blank" rel="noopener noreferrer" draggable="false">
      <Fa icon={faGithub} />
    </a>
  </div>
</nav>

<style>
  * {
    cursor:none;
  }

  #nav-menu {
    display: flex;
    width: 100%;
    border-bottom: 1px solid var(--border-color);
  }
  #nav-menu > .nav-section {
    padding: 0em 0em;
    display: flex;
    gap: 1em;
    border-left: 1px solid var(--border-color);
    align-items: center;
  }

  #nav-link-section,
  #nav-logo-section {
    /* flex-basis is used to calculate how much space will be used by the flex item */
    /* https://www.youtube.com/watch?v=nG2IyH43xMU 2:00 */
    flex-basis: calc(100% / 3);
  }
  #nav-link-section {
    gap: 10rem;
    justify-content: space-evenly;
    letter-spacing: 3px;
  }
  #nav-logo-section {
    justify-content: flex-start;
  }
  #nav-logo-section::before {
    mix-blend-mode: difference;
  }
  #nav-social-section {
    /* useless with one element only but */
    /* for two items, they will grow to share the remaining space */
    flex-grow: 1;
    justify-content: space-evenly;
  }
  #nav-menu a {
    font-weight: 500;
    color: var(--text-color);
    text-decoration: inherit;
    transition: color 0.2s ease-in;
    padding: 2em;
    user-select: none;
    -webkit-user-drag: none;
  }
  #nav-menu a:hover {
    color: rgb(181, 251, 255);
  }
</style>
