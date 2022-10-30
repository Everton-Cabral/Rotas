<template>
    <div class="btnSubmit">
        <div>{{nome}}</div>
        
    </div>
</template>

<script>
export default {
    props:{
        nome:{
            type: String,
            required: true
        }
    }
}
</script>

<style src="./style.scss" lang="scss" scoped />


