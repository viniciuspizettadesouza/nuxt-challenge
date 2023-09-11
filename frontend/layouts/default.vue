<template>
  <UContainer>
    <header>
      <nav class="flex justify-center py-3">
        <NuxtLink to="/">
          <NuxtImg src="/icon.svg" alt="Icon" width="100" height="100" />
        </NuxtLink>
      </nav>
    </header>

    <slot />

    <footer>
      <nav class="flex justify-center py-3">
        <NuxtLink to="/">
          <NuxtImg src="/icon.svg" alt="Icon" width="100" height="100" />
        </NuxtLink>
      </nav>
    </footer>
  </UContainer>
</template>
