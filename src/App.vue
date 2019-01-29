<template>
    <div id="app">
        <HelloWorld/>
    </div>
</template>

<script>
    import HelloWorld from './components/HelloWorld.vue'

    export default {
        name: 'app',
        components: {
            HelloWorld
        }
    }
</script>

<style>
    body {
        background: linear-gradient(to left bottom, hsl(159, 100%, 85%) 0%,hsl(109, 100%, 85%) 100%);
        color: #333;
    }
    #app {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        padding: 60px auto;
        display: flex;
        flex-direction: column;
        justify-items: center;
        min-height: 100vh;
    }
</style>
