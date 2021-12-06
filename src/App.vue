<template>
  <div id="app">
    <h1> This is my first ever PWA Application </h1>
    <img alt="Vue logo" src="./assets/logo.png">
    <button  v-if="updateAvailable" @click="update">Click to update application</button>
    <p> This site is created by Noah Debaere for the Mobile Apps course!</p>
  </div>
</template>

<script>

export default {
  name: 'App',
  components: {
  },
  created() {
    document.addEventListener(
      'swupdatefound', this.updateTheApp, { once: true }
    ); 
  },
  data: () => ({
    registration: null,
    updateAvailable: false
  }),
  methods: {
    updateTheApp(e) {
      this.registration = e.detail
      this.updateAvailable = true;
    },
    update(){ 
      this.updateAvailable =  false; 
      if (this.registration || this.registration.waiting){ 
        this.registration.waiting.postMessage({type:'SKIP_WAITING'});   
      }
    },
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
