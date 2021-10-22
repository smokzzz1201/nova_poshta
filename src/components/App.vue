<template>
   <div style="margin: 50px;">
       <h4>Виберіть місто:</h4>
 <input v-model="ot" >
      
       <button v-on:click="naytiOtdel">Знайти</button>

        <h4>Поштове відділення:</h4>
       <select>
           <option  v-for="ot in otdeli" v-bind:value="ot.Description"  v-bind:key="ot.Cityid">{{ ot.Description}}</option>
       </select>
   </div>
</template>

<script>
    import Vue from 'vue'
    import axios from 'axios'
    import VueAxios from 'vue-axios'
 
   export default {
        data: function() {
           return {
           goroda:[],
           otdeli:[],
           ot:"Запоріжжя",
           
        }},
        mounted: function(){
            
                axios.post("https://api.novaposhta.ua/v2.0/json/Address/getCities", {
                        apiKey: "a296ca247f95d5c0d9755e9b97b2e6a4",
                        modelName: "Address",
                        calledMethod: "getCities",
                        methodProperties: {}
                })
                .then((response)=>{
                    console.log(response.data);
                    this.goroda = response.data.data;
                })            
        },
        methods:{
            naytiOtdel: function() {
                
                 axios.post("https://api.novaposhta.ua/v2.0/json/Address/getWarehouses", {
                        apiKey: "a296ca247f95d5c0d9755e9b97b2e6a4",
                        modelName: "Address",
                        calledMethod: "getWarehouses",
                        methodProperties: {
                            CityName: this.ot,
                        }
                })
                .then((response)=>{
                    console.log(response.data);
                    this.otdeli = response.data.data;
                })
            }
        
        }
    }
</script>
<style scoped>
</style>