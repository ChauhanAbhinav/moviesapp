<template>
 <a-layout>
    <a-layout-header>
      <nav>
        <router-link to="/">
          <h2>Movies Couch</h2>
        </router-link>
      </nav>
    </a-layout-header>
    <a-layout-content>
      <router-view/>
    </a-layout-content>
    <!-- <a-layout-footer></a-layout-footer> -->
  </a-layout>
</template>

<script>
import env from '@/env.js';

export default ({
  setup() {
    if(!env.apikey) {
    alert("Please add your API Key in environments")
    }
  }
})
</script>

<style>
 #app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}
header {
  display: flex;
  align-items: center;
  justify-content: center;
}
.ant-layout-header {
    background: #7dbcea !important;
}
.ant-layout-content {
  min-height: 120px;
  color: #000 !important;
  background: #fff;
}
</style>
