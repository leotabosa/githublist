<template>
    <div class="row">
        <div class="col-sm-4" v-for="repo in repos" :key="repo.id">
            <div class="card">
                <div class="card-body">
                    <h5 class="card-title">{{ repo.name }}</h5>
                    <p class="card-text">
                    <br><b>Número de estrelas:</b> {{ repo.stargazers_count }}
                    <br><b>Linguagem:</b> {{ repo.language }}
                    </p>
                    <a :href="repo.html_url" class="btn btn-dark">Ir para o repositório</a>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    props:['repos']
}
</script>
<style scoped>
.col-sm-4{
    padding-top: 10px;
}
.card{
      border-top:1px solid black;
      border-bottom:1px solid black;
}
.btn-dark{
    background:black;
    border-radius:50px;
    transition:0.4s;
}
.btn-dark:hover{
    background:#3b4a54;
    transition:0.4s;
}
.card-body:hover{
    box-shadow: 10px 10px 1px #3b4a54;
    transition:0.7s;
}
.card-body:not(hover){
    transition:0.7s;
}
</style>


