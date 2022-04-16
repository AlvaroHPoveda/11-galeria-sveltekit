<script lang="ts">
  import ActiveRoute from "./ActiveRoute.svelte";
</script>

<nav class="navbar navbar-expand-lg navbar-dark bg-dark">
  <div class="container-fluid">
    <a class="navbar-brand" href="/">Galeria SK</a>
    <button
      class="navbar-toggler"
      type="button"
      data-bs-toggle="collapse"
      data-bs-target="#navbarNav"
      aria-controls="navbarNav"
      aria-expanded="false"
      aria-label="Toggle navigation"
    >
      <span class="navbar-toggler-icon" />
    </button>
    <div class="collapse navbar-collapse" id="navbarNav">
      <ul class="navbar-nav">
        <li class="nav-item">
          <ActiveRoute route="/">Home</ActiveRoute>
        </li>
        <li class="nav-item">
          <ActiveRoute route="/search">Search</ActiveRoute>
        </li>
      </ul>
    </div>
  </div>
</nav>
