<template>
    
    <div class="wrap">
        <div class="loader"></div>
    </div>
</template>


<style scoped>
    .wrap{
        position:fixed;
        height:100vh;
        width:96.9vw;
        z-index: 1;
    }
    .loader{
        position: fixed;
        background-image: linear-gradient(#abffd0,green);
        border: 16px solid #f3f3f3;
        border-top: 16px solid #abffd0;
        border-right: 16px solid #abffd0;
        border-radius: 50%;
        width: 120px;
        height: 120px;
        animation: spin 2s linear infinite;
        margin: auto;
        left: calc(50% - 60px);
        top: calc(50% - 60px);
        z-index: 1;
    }
    @keyframes spin {
        0% { transform: rotate(0deg); }
        100% { transform: rotate(360deg); }
        }
</style>
