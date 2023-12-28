<template>
    <img :src="computerObject.source">
</template>

<script>
export default {
    props: ['computerObject']
}
</script>

<style scoped>
img {
    height: 5rem;
    width: 5rem;
}
</style>