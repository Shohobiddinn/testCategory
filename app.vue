<script setup lang="ts">
const { isDesktop } = useDevice(); 
</script>

<template>

  <Body>
    <NuxtLayout :name="isDesktop ? 'desktop' : 'mobile'">
      <NuxtPage />
    </NuxtLayout>
  </Body>
</template>
