<template>
  <div id="borderDiv">
    <div id="mainContainer" :style="`transform: scale(${mainContainerOpt.transform});transform-origin: left top 0px;top:${mainContainerOpt.top}px;left:${mainContainerOpt.left}px;`">
      <slot></slot>
    </div>
    <div id="minimap">
      <div id="miniview">
        <slot></slot>
      </div>
      <div id="selectWin" :style="`width:${selectWinOpt.width}px;height:${selectWinOpt.height}px;top:${selectWinOpt.top}px;left:${selectWinOpt.left}px;`"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String
  },
  data() {
    return {
      selectWinOpt: {
        width: "80",
        height: "50",
        top: "0",
        left: "0"
      },
      mainContainerOpt: {
        top: "-0",
        left: "-0",
        transform: "1"
      }
    };
  },
  methods: {
    selectWinDra() {
      let selectionLeft = parseInt($("#selectWin").css("left")),
        selectionTop = parseInt($("#selectWin").css("top"));
      // console.log("selectionLeft", selectionLeft);
      // console.log("selectionTop", selectionTop);
      let multipl = 10 * this.mainContainerOpt.transform;
      this.mainContainerOpt.top = -selectionTop * multipl;
      this.mainContainerOpt.left = -selectionLeft * multipl;
    },

    borderDivMousewheel(event, delta, deltaX, deltaY) {
      let zoom = this.mainContainerOpt.transform;
      if (delta > 0 && zoom <= 1.5) this.mainContainerOpt.transform += 0.05;
      else if (delta < 0 && zoom >= 0.4)
        this.mainContainerOpt.transform -= 0.05;
      else return false;
      this.selectWinOpt.width = 80 / this.mainContainerOpt.transform;
      this.selectWinOpt.height = 50 /this.mainContainerOpt.transform;

    },
    initMiniView() {
      let _this = this;
      $("#selectWin").draggable({
        containment: "parent",
        drag: _this.selectWinDra
      });
      $("#borderDiv").mousewheel(_this.borderDivMousewheel);
    }
  },
  mounted() {
    this.$nextTick(() => {
      this.initMiniView();
    });
  }
};
</script>

<style scoped>
#borderDiv {
  width: 800px;
  height: 500px;
  overflow: hidden;
  left: 100px;
  top: 20px;
  position: relative;
  border: 1px solid #ccc;
}
#mainContainer {
  width: 2000px;
  height: 1500px;
  background: rgb(191, 224, 159, 0.5);
  position: relative;
}
#minimap {
  position: absolute;
  top: 10px;
  right: 10px;
  z-index: 9999;
  width: 200px;
  height: 150px;
  background: rgba(121, 129, 113, 0.5);
}
#miniview {
  transform: scale(0.1);
  transform-origin: left top 0px;
}
#selectWin {
  background: #cccccc89;
  position: relative;
}
</style>
