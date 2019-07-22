<template>
    <div>
        <nav class="navbar navbar-dark bg-custom">
            <a class="navbar-brand" href="">Voltar à página inicial</a>
            <a class="navbar-brand" href="" style="color:white; font-size:22px;">Repositórios da Microsoft</a>
            <a class="navbar-brand" href="https://github.com/Microsoft">GitHub da Microsoft</a>
        </nav>
    </div>
</template>

<style scoped>
    nav{
        border-bottom-left-radius: 20px;
        border-bottom-right-radius: 20px;
    }
    .bg-custom{
        background-color:black;
    }
    .navbar{
        position: relative;
    }
    .navbar-brand:hover{
        font-size:20.5px;
        transition:0.3s;
    }
    .navbar-brand:not(hover){
        font-size:20px;
        transition:0.3s;
    }

</style>

