<script>
  import { Router, Route } from "svelte-navigator";

  import Login from "./lib/Login.svelte";
  import Dashboard from "./lib/Dashboard.svelte";
</script>

<Router>
  <Route path="/"><Login /></Route>
  <Route path="/dashboard"><Dashboard /></Route>
</Router>
