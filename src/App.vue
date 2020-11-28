<template>
  <div id="app">
  </div>
</template>
<script>
import * as THREE from 'three'
// import {OrbitControls} from 'three/examples/jsm/controls/OrbitControls.js';
// import {OBJLoader, MTLLoader} from 'three-obj-mtl-loader';
// import MTLLoader from  'three-mtl-loader';
// import OBJLoader from  'three-obj-loader';
// import {CSS2DRenderer, CSS2DObject} from 'three-css2drender';
//
// const OrbitControls = require('three-orbit-controls')(THREE);
export default {
  name: 'app',
  data() {
    return {
      scene: '',//场景
      camera: '',//摄像机,视角
      renderer: '',//渲染器对象 设置场景的样式  尺寸 背景颜色
      geometry: '',//几何图像
      material: '',//给几何图像的样式
      cube: '',//几何图像与样式结合的3d物体实例
      point: '',//光源
      ambient: ''//环境光
    };
  },
  created() {
    this.init()
    this.animate()

  },

  methods: {
    //初始化
    init() {
      this.scene = new THREE.Scene()
      this.geometry = new THREE.BoxGeometry(100, 100, 100)
      this.material = new THREE.MeshBasicMaterial({color: 0x0000ff})
      this.cube = new THREE.Mesh(this.geometry, this.material);
      this.scene.add(this.cube)
      this.point = new THREE.PointLight( 0xffffff)
      this.point.position.set(400, 200, 300)
      this.scene.add(this.point)
      this.ambient = new THREE.AmbientLight(0x444444)
      this.scene.add(this.ambient)
      console.log(this.scene.children)
      const width = window.innerWidth; //窗口宽度
      const height = window.innerHeight; //窗口高度
      const k = width / height; //窗口宽高比
      const s = 200;
      this.camera = new THREE.OrthographicCamera(-s * k, s * k, s, -s, 1, 1000)
      this.camera.position.set(200, 300, 200)
      this.camera.lookAt(this.scene.position)
      this.renderer = new THREE.WebGLRenderer()
      this.renderer.setSize(window.innerWidth, window.innerHeight)
      this.renderer.setClearColor(0xb9d3ff, 1)
      document.body.appendChild(this.renderer.domElement)

    },
    animate() {
      requestAnimationFrame(this.animate); // 让浏览器执行参数中的函数，不断循环（浏览器一个新的API）
      this.cube.rotation.x += 0.1;
      this.cube.rotation.y += 0.1;
      this.renderer.render(this.scene, this.camera); // 结合场景和相机进行渲染，即用摄像机拍下此刻的场景
    }

  }
}

</script>
<style lang="scss">
#app {
  position: absolute;
  width: 100%;
  height: 100%;
}

body {
  margin: 0;
}

canvas {
  width: 100%;
  height: 100%
}

</style>
