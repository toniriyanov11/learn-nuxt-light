<template>
    <div>
        <h1>USER.</h1>
        <br>
        <div v-if="user">
            <p>{{user.id}},{{user.payload.name}},{{user.payload.job}}</p>
        </div>
        <div v-if="!loading">
            <input type="text" placeholder="name" v-model="name">
            <input type="text" placeholder="job" v-model="job">
        
            <button @click="validateForm('POST')">create user</button>
            <button @click="validateForm('PUT')">edit user</button>
        </div>
        <div v-else>
            loading..
        </div>
    </div> 
</template>

<script>
import axios from 'axios'

export default {
    data(){
        return{
            name:'',
            job:'',
            user:'',
            loading:false
        }
    },
    methods:{
        validateForm:async function (method) {
            if(!this.name){
                alert('name is empty')
            }else if(!this.job){
                alert('job is empty')
            }else{
                this.loading = true
                if(method=='POST'){
                   await this.createUser()
                    
                }else{
                   await this.editUser()
                }
                this.clearForm()
                this.loading = false
            }
        },
        createUser: async function() {
            try{
                let result = await axios.post('https://reqres.in/api/users',{
                        name: this.name,
                        job:  this.job
                })
                console.log(result)
                if(result.status == 201){
                    alert('sukses menambah user')
                }else{
                    alert('gagal menambah user')
                }
            }catch(e){
                alert(e)
            }
        },
        editUser: async function() {
            try{
                let result = await axios.put('https://reqres.in/api/users',{
                        name: this.name,
                        job:  this.job
                } )
                if(result.status == 201){
                    alert('sukses mengedit user')
                }else{
                    alert('gagal  mengedit user')
                }
            }catch(e){
                alert(e)
            }
        },
        clearForm: function(){
            this.name = '',
            this.job = ''
        }
    }
}
</script>