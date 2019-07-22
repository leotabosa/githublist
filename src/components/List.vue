<template>
     <div>
        <div>
            <Card :repos="repos"></Card>      
        </div>
    </div>   
</template>
<script>
import Card from './Card.vue';
export default {
    props: {
        repos: Array
    },
    components:{
        Card,
    },
}
</script>


