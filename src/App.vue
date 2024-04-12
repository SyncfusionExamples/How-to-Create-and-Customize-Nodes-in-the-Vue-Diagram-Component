<template>
  <div class="container" >
    <ejs-button class="button" @click="drawNode">Draw Node</ejs-button>
    <ejs-button class="button" @click="editNode">Edit Node</ejs-button>
    <ejs-button class="button" @click="removeNode">Remove Node</ejs-button>
  </div>
  <ejs-diagram ref="diagramObject" :width="width" :height="height" />
</template>

<script>
import {
  DiagramComponent, DiagramTools
} from '@syncfusion/ej2-vue-diagrams';
import { ButtonComponent } from '@syncfusion/ej2-vue-buttons';

let nodes = [
  {
    offsetX: 300,
    offsetY: 250,
    width: 200,
    height: 100,
    //annotations: [{content: "Basic"},{content: "Rectangle", offset: {y:0.6}}],
    annotations: [{content: "Flow"},{content: "Terminator", offset: {y:0.6}}],
    style: { fill: 'lightblue', strokeColor: 'white'},
    shape: { type:'Flow', shape: 'Terminator'}
  }
];

let diagramInstance;

export default {
  name: 'App',
  components: {
    "ejs-diagram": DiagramComponent,
    "ejs-button": ButtonComponent
  },
  data() {
    return {
      width: '1302px',
      height: '602px',
      //nodes: nodes
      drawNode: () => {
        diagramInstance.tool = DiagramTools.DrawOnce;
        diagramInstance.drawingObject = { shape: { type: 'Basic', shape: 'Rectangle' } };
      },
      editNode: ()=> {
        diagramInstance.nodes[0].width = 400;
        diagramInstance.nodes[0].height = 200;
        diagramInstance.nodes[0].annotations[0].content = "Changed Text";
        diagramInstance.nodes[0].style = { fill: 'Orange', strokeColor: 'Blue' }
      },
      removeNode: ()=> {
        diagramInstance.remove(diagramInstance.nodes[0]);
      }
    };
  },
  mounted: function () {
    diagramInstance = this.$refs.diagramObject.ej2Instances;
    diagramInstance.add(nodes[0]);
  }
};
</script>

<style>
@import '../node_modules/@syncfusion/ej2-vue-diagrams/styles/material.css';
@import '../node_modules/@syncfusion/ej2-vue-buttons/styles/material.css';

.container {
  text-align: left;
  margin-bottom: 10px;
}
.button {
  margin-right: 10px;
}
</style>
