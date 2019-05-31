<template>
  <div id="app">
    <div class="inBody">
      <app-header
        v-on:rebaseValueheader="valueHeader"
      ></app-header>
      <app-body
        :headerState="headerStatus"
      ></app-body>
    </div>
  </div>
</template>

<script lang="ts">
import Header from './components/HeaderComponent.vue'
import Body from './components/BodyComponent.vue'

export default {
  name: "app",
  components: {
    'app-header': Header,
    'app-body': Body
  },
  data() {
    return {
      headerStatus: false
    }
  },
  methods: {
    valueHeader(value) {
      this.headerStatus = value
      console.log('Header Value Received')
    }
  }
};
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Montserrat:400,700');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  outline: none;
}
body {
  background-color: #eeeeee;
  font-family: 'Montserrat', sans-serif;
}
.inBody {
    margin: 30px auto;
    width: 100%;
    max-width: 420px;
}
</style>
