<template>
    <div id="scoreboard">
        <div class="score">
            <h2>{{ playerName }}</h2>
            <p>{{ playerScore }}</p>
        </div>
        <div class="score">
            <h2>Computer</h2>
            <p>{{ computerScore }}</p>
        </div>
    </div>
</template>

<script>
export default {
    props: ['playerScore', 'computerScore', 'playerName']
}
</script>

<style scoped>

#scoreboard {
    display: flex;
    justify-content: space-between;
    padding-left: 3rem;
    padding-right: 4rem;
}

</style>