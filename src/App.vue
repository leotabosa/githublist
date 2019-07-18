<template>
      <div class="wrap">
        <Header></Header>
        <div class="container-fluid">
          <Loader v-if="loading"/>
          
          <div class="row" v-if="!loading">
            <div class="btn-group" role="group" aria-label="Basic example">
              <button type="button" class="btn btn-dark" @click="sort('stargazers_count')" >Estrelas: {{ sortIndicator }}</button>
              <button type="button" class="btn btn-dark" @click="sort('language')">Linguagem</button>
              <form class="form-inline my-2 my-lg-0">
                <input id="1" class="form-control mr-sm-2" type="search" placeholder="Search" aria-label="Search" v-model="searchTerm">
                <button class="btn btn-dark my-2 my-sm-0" @click.prevent="searchResults">Search</button>
              </form>
            </div>
          </div>

          <div class="row" v-if="!loading">
            <div class="col-sm-4" v-for="i in repos" :key="i.id">
              <div class="card">
                <div class="card-body">
                  <h5 class="card-title">{{ i.name }}</h5>
                  <p class="card-text">
                    <br><b>Número de estrelas:</b> {{ i.stargazers_count }}
                    <br><b>Linguagem:</b> {{ i.language }}
                    </p>
                  <a :href="i.html_url" class="btn btn-dark">Ir para o repositório</a>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

</template>

<script>

    import Header from './components/Header.vue';
    import Loader from './components/Loader.vue';
    import Axios from 'axios';
    const axios = Axios.create({
        baseURL: 'https://api.github.com/',
      });
    export default {
        data(){
            return{
                repos: [],
                reposBackup: [],  
                sortPref: { property: "stargazers_count", type: "asc" },
                sortIndicator: "",
                searchTerm: null,
                loading: false
          }
        },
        components: {
            Header,
            Loader
        },
        created(){
            this.setInitialRepos();
        },
        methods:{
          //get e set iniciais
            getInitialRepos() {
                return axios.get('search/repositories?q=org:microsoft');
            },
            async setInitialRepos() {
                const {data} = await this.getInitialRepos();

                this.repos = data.items;
                this.loading = false;
            },
          //função de pesquisa utilizando um get 
            setReposSearch(){
              this.loading = true;
              axios.get('search/repositories',{
                params:{
                  q: 'org:microsoft '+this.searchTerm+' in:name'
                }
              })
                .then(response => {
                  console.log(response);
                  this.repos = response.data.items
                  this.loading = false;
                })
                .catch(err => {
                  console.err(error)
                  this.loading = false;
                })
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
            searchResults(){
              if(this.searchTerm){
                 this.repos = this.setReposSearch();
              }
              else{
                this.loading = true;
                this.repos = this.reposBackup;
                setTimeout(this.setInitialRepos,300);
              } 
            },
          }
        }
    
  
</script>

<style scoped>
    .container-fluid{
        background: #abffd0;
    }
    .col-sm-4{
      padding-top: 10px;
    }
    h2{
      text-align: center;
      padding-top:10px;
    }
    .card{
      border-top:1px solid black;
      border-bottom:1px solid black;
    }
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
    .form-inline{
      padding-left:10px;
    }
    .wrap{
      height:100vh;
      width:100vw;
      background: #abffd0;
    }
</style>
