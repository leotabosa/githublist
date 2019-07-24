<template>
  <div class="wrap">
    <Error v-if="error" :error-message="errorMessage" />
    <Header />
    <Loader v-if="loading" />
    <div class="container">
      <Content
        :repos="mainRepos"
        @onSearch="searchResults($event)"
        @onSort="doSort($event)"
      >
      </Content>
    </div>
    <Footer v-if="!error" />
  </div>
</template>
<script>
import Header from './components/Header.vue'
import Loader from './components/Loader.vue'
import Footer from './components/Footer.vue'
import Content from './components/Content.vue'
import Error from './components/Error.vue'
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
    Error,
  },
  data() {
    return {
      mainRepos: [],
      searchTerm: null,
      loading: true,
      sortPref: {},
      error: false,
      errorMessage: null,
    }
  },
  created() {
    this.setInitialRepos()
  },
  methods: {
    // get e set iniciais
    getInitialRepos() {
      return axios.get('search/repositories?q=org:microsoft').catch((err) => {
        this.loading = false
        this.error = true
        this.errorMessage = err
      })
    },
    async setInitialRepos() {
      const { data } = await this.getInitialRepos()
      this.mainRepos = data.items
      this.loading = false // loading inicia com valor true para essa linha fazer sentido
      this.error = false
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
          this.loading = false
          this.error = true
          this.errorMessage = err
        })
    },
    searchResults(event) {
      this.loading = true
      this.error = false
      if (event) {
        this.mainRepos = this.setReposSearch(event)
      } else {
        this.setInitialRepos()
      }
    },
    doSort(eventData) {
      this.mainRepos.sort((a, b) => {
        var t = eventData.property
        if (eventData.type === 'Decrescente') {
          if (a[t] > b[t]) {
            return -1
          } else {
            return 1
          }
        }
        if (eventData.type === 'Crescente') {
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
