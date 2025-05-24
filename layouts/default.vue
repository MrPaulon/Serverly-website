<template>
    <div>
        <slot />
    </div>
</template>
<script setup>
onMounted(() => {
  document.documentElement.classList.add('dark')
})
</script>