<template>
    <div class="corpo">
        <AppHome />
    </div>
</template>

<script>
import AppHome from './home/AppHome.vue'
export default {
    components: { AppHome}
}
</script>

<style scoped>
.corpo{
    display: flex;
    justify-content: center;
    text-align: center;
    background-image: url('../imagens/mapadefundo.jpg');
    height: 100vh;
   
}
</style>
