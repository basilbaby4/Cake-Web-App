<script>
  import { Router, Route } from "svelte-routing";
  import NavLink from "./components/NavLink.svelte";
  import Home from "./routes/Home.svelte";
  import Cake from "./routes/Cake.svelte";
  import Create from "./routes/Create.svelte";
  // Used for SSR. A falsy value is ignored by the Router.
  export let url = "";
</script>

<Router url="{url}">
  <nav>
    <NavLink to="/">Cakes</NavLink>
  </nav>
  <div>
    <Route path="/" component="{Home}" />
    <Route path="cake/:id" component="{Cake}" />
    <Route path="create" component="{Create}" />
  </div>
</Router>
