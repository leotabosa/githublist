<template>
    <div class="row">
        <div class="btn-group" role="group">
            <button type="button" class="btn btn-dark btn-order" @click="sort('stargazers_count')">Estrelas</button>
            <button type="button" class="btn btn-dark btn-order" @click="sort('language')">Linguagem</button>
            <form class="form-inline my-2 my-lg-0">
            <input class="form-control mr-sm-2" 
            type="search" placeholder="Buscar" 
            v-model="searchTerm" 
            @keydown.enter.prevent.stop="sendSearchTerm">           
            <button type="button" class="btn btn-dark" 
            @click.prevent.stop="sendSearchTerm">Buscar</button>
            </form>
        </div>
    </div>
</template>
<script>
export default {
    data(){
        return{
            sortPref: { 
                property: "stargazers_count", 
                type: "asc",
            },
            searchTerm: null,
        }
    },
    props:['repos'],
    methods:{
        sendSearchTerm(){
            this.$emit('searchTermSet', this.searchTerm);
            this.$emit('setSearchTerm', this.searchTerm);
        },

        // verificações da função de ordenação
        sort (prop) {
            if (this.sortPref.property === prop) {
            this.sortPref.type = this.sortPref.type === 'asc' ? 'desc' : 'asc';
            } else {
            this.sortPref.property = prop;
            this.sortPref.type='desc';  
            }
            this.doSort();
        },
        // função de ordenação
        doSort(){
            this.repos.sort( (a,b) => {
            var t = this.sortPref.property;
                if(this.sortPref.type == 'asc'){
                if(a[t] > b[t]){
                    return -1;
                }
                else{
                    return 1;
                }
                }         
                if(this.sortPref.type == 'desc'){
                if(a[t] > b[t]){
                    return 1;
                }
                else{
                    return -1;
                }
                }  
            });
        },
     }
}
</script>
<style scoped>
.row{
    background:#45f792
}
.btn-group{
    padding-top:10px;
    margin:auto;
    }
.btn-group button{
    border-radius: 50px;
}
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
}
.btn-dark:hover{
    background:#3b4a54;
    transition: 0.4s;
}
.form-inline{
    padding-left:10px;
}
</style>

