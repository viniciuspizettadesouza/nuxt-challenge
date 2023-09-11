<template>
  <UContainer>
    <header>
      <nav>
        <NuxtLink to="/"> Home </NuxtLink>
        <NuxtLink to="/events"> Events </NuxtLink>
      </nav>
    </header>

    <slot />

    <footer>
      <nav>
        <NuxtLink to="/"> Home </NuxtLink>
        <NuxtLink to="/events"> Events </NuxtLink>
      </nav>
    </footer>
  </UContainer>
</template>
