<template>
    <div>
        <Search @ResultSearch="ResultSearch"/>
        <Item 
            v-for="pic in pictures"
            v-bind:key="pic.id"
            v-bind:picture="pic"
        />
    </div>
</template>

<script>
import Search from './Search.vue'
import Item from './Item.vue'

export default {
    name: "Gifs",
    data(){
        return {
            pictures: []
        }
    },
    components: {
        Search,
        Item
    },
    methods:{
        ResultSearch(resp){
            console.log('here: ',resp);
            this.pictures = resp;
        }
    }
}
</script>
