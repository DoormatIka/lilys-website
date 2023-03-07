<script>
  import Main from "./lib/main/Wrapper.svelte"
  import About from "./lib/about/About.svelte"
  import Mouse from "./lib/Mouse.svelte";
  import { Router, Route } from "svelte-routing";
</script>


<Router>
  <Route path="/" component={Main}/>
  <Route path="/about" component={About} />
</Router>