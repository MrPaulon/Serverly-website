<template>
    <div>
        <Navigation />
        <slot />
    </div>
</template>
<script setup>
onMounted(() => {
  document.documentElement.classList.add('dark')
})
</script>