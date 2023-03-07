<script>
  import Nav from "./Nav.svelte"
  import Main from "./Main.svelte"
  import Mouse from "../Mouse.svelte"

</script>

<div id="wrapper">
  <Mouse />
  <Nav />
  <Main />
</div>

<style>
  #wrapper {
    height: 100%;
    width: 100%
  }
</style>