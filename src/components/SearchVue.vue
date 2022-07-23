<template>
  <section>
    <div>
      <h3>搜索</h3>
      <input 
        type="text" 
        placeholder="请输入" 
        @keyup.enter="searchMsg" 
        v-model="keyword" 
      />
    
      &nbsp;
      <button @click="searchMsg">搜索</button>
    </div>

  </section>
</template>

<script>
  import axios from 'axios'
  
  export default {
    name: "SearchVue",
    
    data() {
      return {
        keyword: '',
      }
    },

    methods: {
      searchMsg(){
        this.$bus.$emit("show_Userlist", {
          UserName: [],
          IsFirst: false,
          IsLoad: true,
          ErrMsg: "",
        })

        axios.get(`https://api.github.com/search/users?q=${this.keyword}`).then(
          response => {
            console.log("成功！",response.data)
            this.$bus.$emit("show_Userlist", {
              UserName: response.data.items,
              IsFirst: false,
              IsLoad: false,
              ErrMsg: "",
            })
          },

          error => {
            console.log("失败",error.message)
            this.$bus.$emit("show_Userlist", {
              UserName: [],
              IsFirst: false,
              IsLoad: false,
              ErrMsg: error.message,
            })
          }
        )
      }
    }


  }
</script>

<style scoped>

div {
  text-align: center;
}
</style>