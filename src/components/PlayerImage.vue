<template>
    <img :src="selectedObject.source">
</template>

<script>
export default {
    props: ['selectedObject']
}
</script>

<style scoped>
img {
    height: 5rem;
    width: 5rem;
}
</style>