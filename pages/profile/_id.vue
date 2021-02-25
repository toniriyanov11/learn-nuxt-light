<template>
  <div>
    <h2>Profile</h2>
   <div> <h3>{{id}}</h3><span v-if="id" @click="deleteId"> delete</span></div>
    <input type="text" v-model="message">
    <button @click="findId">find id</button>
    <main v-for="api in resultApi" :key="api.id" >
        <p>{{api.id}}</p>
        <p>{{api.email}}</p>
        <img :src="api.avatar">
    </main>
  </div>  
</template>

<script>
import axios from'axios'

export default {
    //fungsi validasi param
    validate({params}){
        if(params.id){
            return /^\d+$/.test(params.id)
        }else{
            return true
        }
    },
    data(){
        return{
            id : '',
            resultApi:'',
            message:''
        }
    },
    created: function(){
       this.assignId()
       this.callApi()
    },
    mounted(){
        
    },
    methods:{
        assignId: function () {
            this.id = this.$route.params.id
        },
        callApi: async function(){
            if( this.id ){
                let result = await axios.get(`https://reqres.in/api/users/${this.id}`,{})
                let {data} = result.data
                let arr = []
                arr.push(data)
                this.resultApi = arr
                console.log(arr)
            }else{
                console
                let result = await axios.get(`https://reqres.in/api/users?page=1`,{})
                let {data} = result.data
                console.log(data)
                this.resultApi = data
            }
        },
        findId: function(){
            this.$router.push({path:`/profile/${this.message}`})
        },
        deleteId:function(){
            this.id = ''
            this.$router.push({path:`/profile/${this.message}`})
        }
    }
}
</script>