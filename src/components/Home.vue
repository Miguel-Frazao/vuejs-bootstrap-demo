<template>
  <div class="home text-center">
    <h1>{{hello_message}}</h1>
    <p>This simple project was based on <a href="https://bootstrap-vue.js.org/" target="_blank">bootstrap-vue</a></p>
    <b-button target="_blank" variant="primary" href="https://github.com/Miguel-Frazao/vuejs-bootstrap-demo">Github</b-button>
    <br>
    <br>
    <code>git clone https://github.com/Miguel-Frazao/vuejs-bootstrap-demo</code>
    <br>
    <br>
    <b-button target="_blank" variant="primary" href="https://github.com/Miguel-Frazao/vuejs-bootstrap-demo/archive/master.zip" download>Download</b-button>
    <br>
    <br>
    <code>
    cd path/to/this
    <br>
    npm install
    <br>
    npm run dev
    </code>
  </div>
</template>

<script>
export default {
  data() {
    return {
      hello_message: 'Vuejs&Bootstrap demo'
    }
  }
}
</script>

<style scoped>

</style>
