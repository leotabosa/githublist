<template>
<div>
    <Toolbar 
    @searchTermSetting="middleSearchTerm = $event"
    @searchHandle="sendMiddleSearchTerm"
    @sortHandle="middleSortData = $event" 
    @sortTriggered="sendMiddleSortData"></Toolbar>
    <List :repos="repos"></List>
</div>
</template>

<script>
import Toolbar from './Toolbar.vue';
import List from './List.vue';
export default {
    data(){
        return{
            middleSearchTerm: null,
            middleSortData: {}
        }
    },
    props:{
        repos:{
            type: Array,
            required: true,
            default: () => []
        }
    },
    components:{
        Toolbar,
        List
    },
    methods:{
        sendMiddleSearchTerm(){
            this.$emit('searchTermHandle', this.middleSearchTerm);
            this.$emit('searchTrigger');
        },
        sendMiddleSortData(){
            this.$emit('sortHandle', this.middleSortData);
            this.$emit('sortTrigger');
        }
    }
}
</script>
