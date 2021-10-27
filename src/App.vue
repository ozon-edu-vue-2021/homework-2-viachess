
<template>
  <ul id="tree">
    <list-node v-bind:file="fullTree" />
  </ul>
</template>

<script>
import ListNode from './components/ListNode.vue'
// import testTree from '../public/static/babel_test.json';
import fullTree from '../public/static/node_modules.json';


export default {
  name: 'App',
  data: () => {
    return {
    fullTree: fullTree,
  }},
  components: {
    'list-node': ListNode,
  }
}
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding:0;
}
#tree {
  font-family: sans-serif;
  margin-top: 2rem;
  margin-left: 4rem;
}
</style>
