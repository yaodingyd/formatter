<template>
  <div class="container">
    <textarea v-model="input" class="input"></textarea>
    <div class="to">
      <el-button @click="format" class="to-button">Format</el-button>
      <el-button @click="parseCookie" type="primary" class="to-button">Cookie</el-button>
    </div>
    <tree-view :data="jsonSource" :options="{maxDepth: 3}" class="output"></tree-view>
  </div>
</template>

<script>
import TreeView from 'vue-json-tree-view'
import Vue from 'vue'
Vue.use(TreeView)

export default {
  name: 'hello',
  data () {
    return {
      input: '',
      jsonSource: ''
    }
  },
  methods: {
    format: function () {
      var json = '{"' + this.input.replace(/[,]?[\s]?$/, '').replace(/[,]/g, '", "').replace(/=/g, '": "') + '"}'
      this.jsonSource = JSON.parse(json)
    },
    parseCookie: function () {
      let output = {}
      this.input.split(/\s*;\s*/).forEach(function (pair) {
        pair = pair.split(/\s*=\s*/)
        output[pair[0]] = pair.splice(1).join('=')
      })
      this.jsonSource = output
    }
  }
}
</script>

<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}

.container {
  position: relative;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.input {
  width: 35%;
  height: 100vh;
  display: block;
  margin-right: 2%;
}

.to-button {
  height: 60px;
  font-size: 20px;
  margin: 20px auto;
  display: block
}

.output {
  text-align: left;
  width: 50%;
  height: 100vh;
  margin-left: 2%;
  display: block;
  border: 1px solid #000;
}

</style>
