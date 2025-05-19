<script lang="ts">
    import { Toaster } from "svelte-sonner";
    import Router from "svelte-spa-router";
    import { current } from "./lib/Pocketbase.svelte";
    import Navbar from "./components/Navbar.svelte";
    import Dashboard from "./Routes/Dashboard/Dashboard.svelte";
    import Login from "./Routes/Login/Login.svelte";

    const routes = {
      "/" : Dashboard,
      "*" : Dashboard
    }

</script>

<div class="max-w-[700px] mx-auto">
    <Navbar/>
    {#if !current.user}
        <Login/>
    {:else}
        <Router routes = { routes }/>
    {/if}
</div>

<Toaster position="bottom-right" expand={false} richColors closeButton/>