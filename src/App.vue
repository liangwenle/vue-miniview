<template>
  <div id="app">
    <HelloWorld msg="ok">
      <div slot-scope="slotProps">
        <div 
        v-for="(node,index) in nodes" 
        :key="index" 
        :id="`node_${index}`" 
        class="node" 
        :style="`top:${node.top}px;left:${node.left}px`">
          {{node.title}}
        </div>
      </div>
    </HelloWorld>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";

export default {
  name: "app",
  components: {
    HelloWorld
  },
  data() {
    return {
      nodes: [
        {
          title: "a",
          top: "10",
          left: "10"
        },
        {
          title: "a",
          top: "470",
          left: "60"
        },
        {
          title: "a",
          top: "1400",
          left: "1900"
        }
      ]
    };
  },
  methods:{
    addNode(){
      this.nodes.push({
          title: "b",
          top: "370",
          left: "160"
      })
    }
  }
};
</script>

<style>
* {
  /* padding: 0;
  margin: 0; */
}
.node {
  width: 100px;
  height: 80px;
  background: #74ab6c;
  border: 2px solid #fff;
  position: absolute;
  text-align: center;
  line-height: 80px;
}
</style>
