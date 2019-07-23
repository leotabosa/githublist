<template>
    <form class="form-inline my-2 my-lg-0">
        <input class="form-control mr-sm-2" 
        type="search" placeholder="Buscar" 
        v-model="searchTerm" 
        @keydown.enter.prevent.stop
        @keydown="setTime(sendSearchTerm)">           
    </form>
</template>
<script>
export default {
    data(){
        return{
            searchTerm: null,
        }
    },
    methods:{
        sendSearchTerm(){
            this.$emit('searchTermSet', this.searchTerm);
            this.$emit('handleSearchTerm');
        },
        setTime(func){
            clearTimeout(this.interval);
            this.interval = setTimeout(func,500);
        }
    }
}
</script>
<style scoped>
.form-control:focus{
    border-radius: 50px;
    transition: 0.8s;
}
.form-control:not(:focus){
    border-radius: 0px;
    transition: 0.4s;
}
.btn-dark{
    background:black;
    transition: 0.4s;
    border-top-right-radius: 20px;
    border-bottom-right-radius: 20px;
}
.btn-dark:hover{
    background:#3b4a54;
    transition: 0.4s;
}
.form-inline{
    padding-left:10px;
    margin-right:auto;
}
</style>


