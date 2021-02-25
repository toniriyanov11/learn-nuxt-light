<template>
  <div class="container">
    <div>
      <h1 >
        learn-nuxt-light
      </h1>
      <p>{{test}}</p>
      <div class="links">
        <a
        @click="callApi"
        class="button--green">
          Call API
        </a>
      </div>
    </div>
  </div>
</template>

<script>
import axios from'axios'

export default {
  data(){
    return{
      test : 'ini test'
    }
  },
  methods:{
    callApi: async function(){
      this.test = 'calling api...'
      console.log(this)
      setTimeout(async ()=>{
        console.log(this)
        let result = await axios.get('https://reqres.in/api/users?page=2',{})
        let {data} = result.data
        this.test = data.map((item)=>{
            return item.email
          })
      },2000)
    }
  }
}
</script>

