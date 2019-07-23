<template>
  <div class="wrap">
    <Header></Header>
    <Loader v-if="loading"></Loader>
    <div class="container">
      <Content
        :repos="mainRepos"
        @onSearch="searchResults($event)"
        @onSort="doSort($event)"
      >
      </Content>
    </div>
    <Footer class="footer"></Footer>
  </div>
</template>
<script>
import Header from './components/Header.vue'
import Loader from './components/Loader.vue'
import Footer from './components/Footer.vue'
import Content from './components/Content.vue'
import Axios from 'axios'
const axios = Axios.create({
  baseURL: 'https://api.github.com/',
})
export default {
  components: {
    Header,
    Loader,
    Footer,
    Content,
  },
  data() {
    return {
      mainRepos: [],
      searchTerm: null,
      loading: true,
      sortPref: {},
    }
  },
  created() {
    this.setInitialRepos()
  },
  methods: {
    // get e set iniciais
    getInitialRepos() {
      return axios.get('search/repositories?q=org:microsoft')
    },
    async setInitialRepos() {
      const { data } = await this.getInitialRepos()
      this.mainRepos = data.items
      this.loading = false // loading inicia com valor true para essa linha fazer sentido
    },
    // get e set da busca (chamados pelo evento setSearchTerm do botão/input)
    setReposSearch(eventData) {
      axios
        .get('search/repositories', {
          params: {
            q: 'org:microsoft ' + eventData + ' in:name',
          },
        })
        .then((response) => {
          this.mainRepos = response.data.items
          this.loading = false
        })
        .catch((err) => {
          console.err(err)
          this.loading = false
        })
    },
    searchResults(event) {
      this.loading = true
      if (event) {
        this.mainRepos = this.setReposSearch(event)
      } else {
        this.setInitialRepos()
      }
    },
    doSort(event) {
      this.mainRepos.sort((a, b) => {
        var t = event.property
        if (event.type == 'asc') {
          if (a[t] > b[t]) {
            return -1
          } else {
            return 1
          }
        }
        if (event.type == 'desc') {
          if (a[t] > b[t]) {
            return 1
          } else {
            return -1
          }
        }
      })
    },
  },
}
</script>

<style scoped>
.wrap {
  height: 100%;
  background-image: linear-gradient(#45f792, #ffffff);
}
</style>
