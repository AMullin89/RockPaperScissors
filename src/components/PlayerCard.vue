<template>
    <div id="player-buttons">
        <base-button @click="selectRock" >Rock</base-button>
        <base-button @click="selectPaper">Paper</base-button>
        <base-button @click="selectScissors">Scissors</base-button>
    </div>
</template>

<script>
export default {
    methods: {
        selectRock(){
            console.log('Rock')
            this.$emit('select-rock')
        },
        selectPaper() {
            console.log('Paper')
            this.$emit('select-paper')
        },
        selectScissors() {
            console.log('Scissors')
            this.$emit('select-scissors')
        }
    }
    
}
</script>

<style scoped>

#player-buttons {
    display: flex;
    align-items: center;
    justify-content: space-evenly;
    flex-direction: column;
    width: 10rem;
    height: 15rem;
    background-color: rgb(120, 120, 237);
    border-radius: 10px;
    box-shadow: 2px 2px 10px black;
    margin-right: 2rem;
    
}

</style>