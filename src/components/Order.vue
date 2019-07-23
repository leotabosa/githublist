<template>
    <div class="btn-group" role="group">
        <button type="button" 
        class="btn btn-dark btn-order" 
        @click="sort('stargazers_count')">Estrelas
        </button>
        <button type="button" 
        class="btn btn-dark btn-order" 
        @click="sort('language')" 
        style="border-radius:2px">Linguagem
        </button>
    </div>
</template>

<script>
export default {
    data(){
        return{
            sortPref: { 
                property: "stargazers_count", 
                type: "asc"
            },
        }
    },
    methods:{
        // verificações da função de ordenação
        sort (prop) {
            if (this.sortPref.property === prop) {
            this.sortPref.type = this.sortPref.type === 'asc' ? 'desc' : 'asc';
            } else {
            this.sortPref.property = prop;
            this.sortPref.type='desc';  
            }
            this.$emit('sortDataSet',this.sortPref);
            this.$emit('handleSortData');
        },
     }
}
</script>

<style scoped>
.btn-group{
    padding-left:10px;
    margin-left: auto;
    }
.btn-group button{
    border-radius: 20px;
}
.btn-dark{
    background:black;
    transition: 0.4s;
}
.btn-dark:hover{
    background:#3b4a54;
    transition: 0.4s;
}
</style>
