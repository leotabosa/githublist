<template>
    <div class="row" v-if="!loadingIndicator">
            <div class="btn-group" role="group" aria-label="Basic example">
              <button type="button" class="btn btn-dark" @click="sort('stargazers_count')" >Estrelas</button>
              <button type="button" class="btn btn-dark" @click="sort('language')">Linguagem</button>
              <form class="form-inline my-2 my-lg-0">
                <input id="1" class="form-control mr-sm-2" type="search" placeholder="Search" aria-label="Search" v-model="searchTerm">
                <button class="btn btn-dark my-2 my-sm-0" @click.prevent="searchResults">Search</button>
              </form>
            </div>
          </div>
</template>
<script>
import App from '../App.vue';
import Axios from 'axios';
    const axios = Axios.create({
        baseURL: 'https://api.github.com/',
      });
export default {
    data(){
        return{
            searchTerm: null,
            loadingIndicator: this.loading,
            reposSearch: this.repos
        }
    },
    props:{
        sortPref: Object,
        loading: Boolean,
        repos: Array
    },
    methods:{
        setReposSearch(){
            this.loadingIndicator = true;
            axios.get('search/repositories',{
            params:{
                q: 'org:microsoft '+this.searchTerm+' in:name'
            }
            })
            .then(response => {
                console.log(response);
                this.reposSearch = response.data.items
                this.loadingIndicator = false;
            })
            .catch(err => {
                console.err(error)
                this.loadingIndicator = false;
            })
        },
        // verificações da função de ordenação
        sort (prop) {
            if (this.sortPref.property === prop) {
            this.sortPref.type = this.sortPref.type === 'asc' ? 'desc' : 'asc';
            console.log(this.sortPref.type)
            } else {
            this.sortPref.property = prop;
            this.sortPref.type='desc';  
            console.log(this.sortPref.property)
            }
            this.doSort();
        },
        // função de ordenação
        doSort(){
            this.reposSearch.sort( (a,b) => {
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
        searchResults(event){
            if(this.searchTerm){
                this.reposSearch = this.setReposSearch();
            }
            else{
            this.loadingIndicator = true;
            this.reposSearch = this.reposBackup;
            setTimeout(this.setInitialRepos,300);
            } 
        },
    }
}
</script>

<style <style scoped>
    
    .btn-group{
      padding-top:10px;
      margin:auto;
    }
    .btn-dark{
      background:black;
    }
    .btn-dark:hover{
      background:#3b4a54;
    }
</style>

