<template>
  <div class="home">
    <img
      alt="Vue logo"
      src="https://img1.baidu.com/it/u=656415248,1056069636&fm=253&fmt=auto&app=138&f=JPEG?w=500&h=500"
    />
    <HelloWorld msg="那年我双手插兜，不知道什么叫对手" />
    <p>{{info}}</p>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";
export default {
  name: "HomeView",
  data() {
    return {
      info:''
    }
  },
  components: {
    HelloWorld,
  },
  mounted() {
    console.log(this.$electron);
  }
};
</script>
