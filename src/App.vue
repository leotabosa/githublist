<template>
    <div class="wrap">
      <Header></Header>
      <Loader v-if="loading"></Loader>
      <div class="container">
        <SearchOrder :repos="mainRepos" @searchTermSet="searchTerm=$event" @setSearchTerm="searchResults"></SearchOrder>
        <List :repos="mainRepos"></List>
        </div>
      <Footer></Footer>
    </div>
</template>

<script>
    import Header from './components/Header.vue';
    import List from './components/List.vue';
    import SearchOrder from './components/SearchOrder.vue';
    import Loader from './components/Loader.vue';
    import Footer from './components/Footer.vue';
    import Axios from 'axios';
    const axios = Axios.create({
        baseURL: 'https://api.github.com/',
      });
    export default {
        data(){
            return{
                mainRepos: [],
                searchTerm: null,
                searchRepos: [],
                loading: true
          }
        },
        components: {
            Header,
            List,
            SearchOrder,
            Loader,
            Footer
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
            this.mainRepos = data.items;
            this.loading = false; //loading inicia com valor true para essa linha fazer sentido
        },
        //get e set da busca (chamados pelo evento setSearchTerm do botão/input)
        setReposSearch(){
          axios.get('search/repositories',{
              params:{
                  q: 'org:microsoft '+this.searchTerm+' in:name'
              }
          })
              .then(response => {
                this.mainRepos = response.data.items
                this.loading = false;
              })
              .catch(err => {
                console.err(err)
                this.loading = false;
              })
          },
        searchResults(){
            this.loading = true;
            if(this.searchTerm){
                this.mainRepos = this.setReposSearch();                
            }
            else{
                this.setInitialRepos();
            } 
        },     
      }
    }
</script>

<style scoped>
.wrap{
    height:100%;
    width:100%;
    background-image: linear-gradient(#45f792,#ffffff);
}
</style>
