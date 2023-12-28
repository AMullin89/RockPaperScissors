<template>
    <button>
        <slot></slot>
    </button>
</template>

<script>
export default {
    
}
</script>

<style scoped>
 button {
    width: 5rem;
    height: 2rem;
    border-radius: 5px;
    border: none;
    box-shadow: 2px 2px 10px black;
    font-family: 'Roboto', sans-serif;
    font-size: 1.1rem;
    background-color: rgb(62, 62, 147);
    color: white;
 }

 button:hover {
    cursor: pointer;
    background-color: rgb(81, 81, 147);
 }

 button:focus {
    border: 2px solid black;
 }
</style>