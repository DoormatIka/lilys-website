<script>
  import { spring } from "svelte/motion";
  let coords = spring({ x: 0, y: 0 }, {
    stiffness: 0.05,
    damping: 0.25
  });
  let main_coords = spring({ x: 0, y: 0 }, {
    stiffness: 0.3,
    damping: 0.8
  })
  let size = spring(25, { stiffness: 0.05, damping: 0.2 });
  let main_size = spring(10);

  let called = true;
  window.onmousemove = (e) => {
    const a = e.target.closest("a");
    const interacting = a !== null;
    const sub_mouse = document.getElementById("sub-mouse");

    if (interacting) {
      size.set(1);
      sub_mouse.style.display = "none";
      main_size.set(40);
      called = false;
    } else {
      if (called) { return; }

      size.set(20)
      sub_mouse.style.display = "block";
      main_size.set(10)

      called = true;
    }
  }
</script>

<!-- To run the svelte code on the window itself! -->
<svelte:window
  on:mousemove={(e) => {
    coords.set({ x: e.pageX + 9, y: e.pageY + 10 })
    main_coords.set({ x: e.pageX + 9 , y: e.pageY + 10 })
  }}
  on:mousedown={(e) => {
    size.update(c => c + 10)
    main_size.update(c => c + 15)
  }}
  on:mouseup={(e) => {
    size.update(c => c - 10)
    main_size.update(c => c - 15)
  }}
/>

<svg>
  <circle cx={$coords.x} cy={$coords.y} r={$size} id="sub-mouse" />
  <circle cx={$main_coords.x} cy={$main_coords.y} r={$main_size} id="main-mouse" />
</svg>

<style>
  svg {
    width: 100%;
    height: 100%;
    margin: -8px;
    position: absolute;
    pointer-events: none;
    mix-blend-mode:difference;
  }

  #sub-mouse {
    stroke: #e6c56a;
    fill-opacity: 0;
  }
  #main-mouse {
    fill: #fffbf1;
  }
</style>