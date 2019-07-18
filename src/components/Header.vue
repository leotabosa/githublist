<template>
    <div>
        <nav class="navbar navbar-dark bg-custom">
            <a class="navbar-brand" href="">Voltar à página inicial</a>
            <a class="navbar-title" style="color:white; font-size:22px; text-shadow:1px 1px 1px black">Repositórios da Microsoft</a>
            <a class="navbar-brand" href="https://github.com/Microsoft">GitHub da Microsoft</a>
        </nav>
    </div>
</template>
<script>
export default {
    
}
</script>
<style scoped>
    nav{
        border-bottom-left-radius: 20px;
        border-bottom-right-radius: 20px;
    }
    .bg-custom{
        background-color:black;
    }
    .navbar-brand:hover{
        padding-top:10px;
        -webkit-transition:0.3s;
    }
    .navbar-brand:not(:hover){
        padding-top:0px;
        -webkit-transition: 0.3s;
    }
    .navbar{
        position: relative;
    }
</style>

