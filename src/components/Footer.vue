<template>
    <div class="footer-wrap">
        <a href="" class="footer-link"><h6 class="footer-text-1">Repositórios da Microsoft</h6></a>
    </div>
</template>
<script>
export default {
    
}
</script>
<style scoped>
    .footer-wrap{
        margin-top:30px;
        height: 5vh;
        background-color: black;
        border-top: 3px solid green;
        text-align:center;
    }
    .footer-text-1{
        padding-top: 6px;
        color:#45f792;
        text-align:center;
        transition:0.2s;
        display: inline-block;
    }
    .footer-text-1:hover{
        color: white;
        transition:0.2s;
    }
    .footer-link:hover{
        text-decoration: none;
    }
</style>
