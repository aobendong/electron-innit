<template>
  <div id="app">
    <navi class="navi"></navi>
    <audio
      :autoplay="true"
      controls
      src="http://m701.music.126.net/20221220125922/a147312b2fc525e970a106d0ac07521f/jdyyaac/obj/w5rDlsOJwrLDjj7CmsOj/17718435852/97a3/1654/3e5e/1f8b83378352fb48773c53d1cff2ea6f.m4a"
      style="position: relative; z-index: 90;"
    ></audio>
    <nav>
      <router-link to="/">说不清，可能是路由</router-link> |
      <router-link to="/about">点点试试</router-link>
    </nav>
    <router-view/>
  </div>
</template>
<script>
import Navi from './components/navi.vue'
export default {
  components:{
    Navi
  },
  data() {
    return {
      
    }
  },

}
</script>
<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  .navi{
  margin-bottom: 50px;
  position: sticky;
  top: 0px;
  }
}

nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
