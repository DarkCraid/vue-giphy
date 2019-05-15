<template>
    <div>
        <form @submit.prevent="onSubmit">
            <input type="text" v-validate="'required|min:5'" placeholder="Busca un gif" v-model="field" name="field">
            <span>{{ errors.first('field') }}</span>
            <button type="submit">Buscar</button>
        </form>
    </div>
</template>

<script>
import Axios from 'axios'

export default {
    name: "Search",
    data(){
        return {
            field: '',
            list: []
        }
    },
    methods:{
        onSubmit(){
            this.$validator.validate().then(valid => {
                if(valid){
                    Axios.get(`http://api.giphy.com/v1/gifs/search?q=${this.field}&api_key=L5g8BmyVeKgYC5ey2sBCPTCs71mjAt6h&limit=5`).then(resp => {
                        let response = resp.data.data;
                        this.list = [];

                        console.log('result: ',response);
                        for(let [i, v] of response.entries()){
                            var obj = {
                                id: i,
                                url: v.url,
                                img: v.images.preview_gif.url
                                };
                            this.list.push(obj);
                            //console.log(i,v);
                        }
                        
                        this.$emit('ResultSearch',this.list);
                    });
                }else{
                    console.log("algo esta mal ",valid);
                }
            }).catch(err => console.log(err));
        }
    }

}
</script>

<style>
 form input{
    max-width: 300px;
    border-radius: 2px;
    border: 1px solid #c5c5c5;
 }
 form > *{
    padding: 10px;
    font-size: 20px;
 }
</style>
