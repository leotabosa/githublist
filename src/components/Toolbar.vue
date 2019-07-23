<template>
    <div class="row">
        <Order
        @sortDataSet="sortData = $event" 
        @handleSortData="sortTrigger">
        </Order>
        <Search 
        @searchTermSet="searchTerm=$event" 
        @handleSearchTerm="searchTrigger" 
        ></Search>
    </div>
</template>
<script>
    import Search from './Search.vue';
    import Order from './Order.vue';
    export default {
        data(){
            return{
                searchTerm: null,
                sortData: {}
            }
        },
        components:{
            Search,
            Order
        },
        methods:{
            searchTrigger(){
                this.$emit('searchTermSetting', this.searchTerm);
                this.$emit('searchHandle');
            },
            sortTrigger(){
                this.$emit('sortHandle', this.sortData);
                this.$emit('sortTriggered');
            }
        }
}
</script>
<style scoped>
    .row{
        padding-top:10px;
        width:100%;
    }
</style>
