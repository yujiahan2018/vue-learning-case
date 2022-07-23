<template>
  <div>

    <div id="list" v-for="user in Info.UserName" :key="user.id">
      <a :href="user.html_url">
        <img :src="user.avatar_url">
      </a>
      <p><span>{{ user.login }}</span></p>
    </div>

    <div id="promsg">
      <h1 v-show="Info.IsFirst">欢迎使用</h1>
      <h1 v-show="Info.IsLoad">Message is Loading...</h1>
      <h1 v-show="Info.ErrMsg">Error: {{ Info.ErrMsg }}</h1>
    </div>
  </div>

</template>

<script>
  export default {
    name: "ListVue",

    data() {
      return {
        Info:{
          UserName: [],
          IsFirst: true,
          IsLoad: false,
          ErrMsg: "",
        },
      }
    },

    mounted() {
      this.$bus.$on("show_Userlist",(userdata)=>{
        // console.log("调用回调")
        console.log(userdata)
        this.Info = {...this.Info,...userdata}
      })
    }
  }
</script>

<style scoped>

  div#list{
    /* width: 10rem; */
    /* background-color: aqua; */
    display: inline-table;
    padding: 2px;
    text-align: center;
  }

  img{
    width: 10rem;
  }

  div#promsg{
    text-align: center;
  }

</style>