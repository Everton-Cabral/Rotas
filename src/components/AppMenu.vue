<template>
    <div class="menu">
        <img src="../icons/home.png" alt="Home">
        <img src="../icons/cozinhando.png" alt="Preparando">
        <img src="../icons/prontoVerde.png" alt="Pronto">
        <img src="../icons/prontoAmarelo.png" alt="Pronto-Atenção">
        <img src="../icons/prontoVermelho.png" alt="Pronto-Atrasado">
        <img src="../icons/entregando.png" alt="Entregando">
    </div>
</template>

<script>
export default {

}
</script>

<style scoped>
.menu{
    background-color:#433F45;
    height: 100vh;
    width: 5%;
    border-radius: 10px;
    margin-right: 8px; 
    display: flex;
    flex-direction: column;
    align-items: center;
}
img {
    height: 60px;
    margin-top: 10px;
    width: 60px;
}
</style>
