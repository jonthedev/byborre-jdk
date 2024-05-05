<template>
  <nav class="navbar" id="navbar" data-testid="navbar">
    <div class="navbar__logo">
      <h1 class="navbar__logo__text">BYBORRE<span class="logo__trademark">&reg;</span></h1>
    </div>
  </nav>
</template>

<style scoped>
.navbar {
  @apply absolute top-0 z-10 h-16 shadow-sm shadow-slate-950 px-6 flex items-center min-w-full;
}

.navbar__logo__text {
  @apply mr-auto font-extrabold text-xl tracking-wide relative;
}

.logo__trademark {
  @apply absolute top-0.5 text-xs font-normal;
}
</style>
