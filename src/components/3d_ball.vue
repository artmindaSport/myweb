<template>
  <div id="container"></div>
</template>

<script>
import * as THREE from "three";
// import Stats from "./stats.module.js";
// import { GUI } from "./dat.gui.module.js";
// import { OrbitControls } from './OrbitControls.js';
import { OBJLoader, MTLLoader } from "three-obj-mtl-loader";
// import MTLLoader from  'three-mtl-loader';
// import OBJLoader from  'three-obj-loader';
import { CSS2DRenderer, CSS2DObject } from "three-css2drender";
const OrbitControls = require("three-orbit-controls")(THREE);

export default {
  name: "Home",
  data() {
    return {
      group: "",
      container:"",
      stats: "",
      particlesData: [],
      camera: "",
      scene: "",
      renderer: "",
      positions:"",
      colors: "",
      particles: "",
      pointCloud: "",
      particlePositions: "",
      linesMesh: "",
      maxParticleCount: 1000,
      particleCount: 300,
      r: 800,
      rHalf: 100 / 2,
      effectController:{
        showDots: false,
        showLines: true,
        minDistance: 150,
        limitConnections: false,
        maxConnections: 8,
        particleCount: 345
      }
    }
  },
  methods: {
    // initGUI(){
    //   var gui = new GUI();

    //   gui.add(this.effectController, this.effectController.showDots).onChange(function(value) {
    //     pointCloud.visible = value;
    //   });
    //   gui.add(this.effectController, this.effectController.showLines).onChange(function(value) {
    //     linesMesh.visible = value;
    //   });
    //   gui.add(this.effectController, this.effectController.minDistance, 10, 300);
    //   gui.add(this.effectController, this.effectController.limitConnections);
    //   gui.add(this.effectController, this.effectController.maxConnections, 0, 30, 1);
    //   gui
    //     .add(this.effectController, this.effectController.particleCount, 0, maxParticleCount, 1)
    //     .onChange(function(value) {
    //       particleCount = parseInt(value);
    //       particles.setDrawRange(0, particleCount);
    //     });
    // },

    init() {
    //   this.initGUI();

      this.container = document.getElementById("container");

      this.camera = new THREE.PerspectiveCamera(
        60,
        window.innerWidth / window.innerHeight,
        1,
        4000
      );
      this.camera.position.z = 2000;
   
      var controls = new OrbitControls(this.camera, this.container);

      this.scene = new THREE.Scene();

      this.group = new THREE.Group();
      this.scene.add(this.group);

      var helper = new THREE.BoxHelper(
        new THREE.Mesh(new THREE.BoxBufferGeometry(this.r, this.r, this.r))
      );
      helper.material.color.setHex(0x101010);
      helper.material.blending = THREE.AdditiveBlending;
      helper.material.transparent = true;
      this.group.add(helper);

      var segments = this.maxParticleCount * this.maxParticleCount;

      this.positions = new Float32Array(segments * 3);
      this.colors = new Float32Array(segments * 3);

      var pMaterial = new THREE.PointsMaterial({
        color: 0x222222,
        size: 3,
        blending: THREE.AdditiveBlending,
        transparent: true,
        sizeAttenuation: false
      });

      this.particles = new THREE.BufferGeometry();
      this.particlePositions = new Float32Array(this.maxParticleCount * 3);

      for (var i = 0; i < this.maxParticleCount; i++) {
        var x = Math.random() *this.r-this.r/ 2;
        var y = Math.random() *this.r-this.r/ 2;
        var z = Math.random() *this.r-this.r/ 2;

        this.particlePositions[i * 3] = x;
        this.particlePositions[i * 3 + 1] = y;
        this.particlePositions[i * 3 + 2] = z;

        // add it to the geometry
        this.particlesData.push({
          velocity: new THREE.Vector3(
            -1 + Math.random() * 2,
            -1 + Math.random() * 2,
            -1 + Math.random() * 2
          ),
          numConnections: 0
        });
      }

      this.particles.setDrawRange(0, this.particleCount);
      this.particles.setAttribute(
        "position",
        new THREE.BufferAttribute(this.particlePositions, 3).setUsage(
          THREE.DynamicDrawUsage
        )
      );

      // create the particle system
      this.pointCloud = new THREE.Points(this.particles, pMaterial);
      this.group.add(this.pointCloud);

      var geometry = new THREE.BufferGeometry();

      geometry.setAttribute(
        "position",
        new THREE.BufferAttribute(this.positions, 3).setUsage(THREE.DynamicDrawUsage)
      );
      geometry.setAttribute(
        "color",
        new THREE.BufferAttribute(this.colors, 3).setUsage(THREE.DynamicDrawUsage)
      );

      geometry.computeBoundingSphere();

      geometry.setDrawRange(0, 0);


      var material = new THREE.LineBasicMaterial({
        vertexColors: THREE.VertexColors,
        blending: THREE.AdditiveBlending,
        transparent: true
      });

      this.linesMesh = new THREE.LineSegments(geometry, material);
      this.group.add(this.linesMesh);

      //

      this.renderer = new THREE.WebGLRenderer({ antialias: true });
      this.renderer.setPixelRatio(window.devicePixelRatio);
      this.renderer.setSize(window.innerWidth, window.innerHeight);
      this.renderer.outputEncoding = THREE.sRGBEncoding;

      this.container.appendChild(this.renderer.domElement);

      //

    //   this.stats = new Stats();
    //   this.container.appendChild(this.stats.dom);

      window.addEventListener("resize", this.onWindowResize, false);
    },

    onWindowResize() {
      this.camera.aspect = window.innerWidth / window.innerHeight;
      this.camera.updateProjectionMatrix();

      this.renderer.setSize(window.innerWidth, window.innerHeight);
    },

    animate() {
      var vertexpos = 0;
      var colorpos = 0;
      var numConnected = 0;

      for (var i = 0; i < this.particleCount; i++)
        this.particlesData[i].numConnections = 0;

      for (var i = 0; i < this.particleCount; i++) {
        // get the particle
        var particleData = this.particlesData[i];

        this.particlePositions[i * 3] += particleData.velocity.x;
        this.particlePositions[i * 3 + 1] += particleData.velocity.y;
        this.particlePositions[i * 3 + 2] += particleData.velocity.z;

        if (
          this.particlePositions[i * 3 + 1] < -this.rHalf ||
          this.particlePositions[i * 3 + 1] > this.rHalf
        )
          particleData.velocity.y = -particleData.velocity.y;

        if (
          this.particlePositions[i * 3] < -this.rHalf ||
          this.particlePositions[i * 3] > this.rHalf
        )
          particleData.velocity.x = -particleData.velocity.x;

        if (
          this.particlePositions[i * 3 + 2] < -this.rHalf ||
          this.particlePositions[i * 3 + 2] > this.rHalf
        )
          particleData.velocity.z = -particleData.velocity.z;

        if (
          this.effectController.limitConnections &&
          particleData.numConnections >= this.effectController.maxConnections
        )
          continue;

        // Check collision
        for (var j = i + 1; j < this.particleCount; j++) {
          var particleDataB = this.particlesData[j];
          if (
            this.effectController.limitConnections &&
            particleDataB.numConnections >= this.effectController.maxConnections
          )
            continue;

          var dx = this.particlePositions[i * 3] - this.particlePositions[j * 3];
          var dy = this.particlePositions[i * 3 + 1] - this.particlePositions[j * 3 + 1];
          var dz = this.particlePositions[i * 3 + 2] - this.particlePositions[j * 3 + 2];
          var dist = Math.sqrt(dx * dx + dy * dy + dz * dz);

          if (dist < this.effectController.minDistance) {
            particleData.numConnections++;
            particleDataB.numConnections++;

            var alpha = 1.0 - dist / this.effectController.minDistance;

            this.positions[vertexpos++] = this.particlePositions[i * 3];
            this.positions[vertexpos++] = this.particlePositions[i * 3 + 1];
            this.positions[vertexpos++] = this.particlePositions[i * 3 + 2];

            this.positions[vertexpos++] = this.particlePositions[j * 3];
            this.positions[vertexpos++] = this.particlePositions[j * 3 + 1];
            this.positions[vertexpos++] = this.particlePositions[j * 3 + 2];

            this.colors[colorpos++] = alpha;
            this.colors[colorpos++] = alpha;
            this.colors[colorpos++] = alpha;

            this.colors[colorpos++] = alpha;
            this.colors[colorpos++] = alpha;
            this.colors[colorpos++] = alpha;

            numConnected++;
          }
        }
      }

      this.linesMesh.geometry.setDrawRange(0, numConnected * 2);
      this.linesMesh.geometry.attributes.position.needsUpdate = true;
      this.linesMesh.geometry.attributes.color.needsUpdate = true;

      this.pointCloud.geometry.attributes.position.needsUpdate = true;

      requestAnimationFrame(this.animate);

    //   this.stats.update();
      this.render();
    },

    render() {
      var time = Date.now() * 0.001;

      this.group.rotation.y = time * 0.1;
      this.renderer.render(this.scene, this.camera);
    }
  },
  mounted() {
    this.init()
    this.animate()
  }
};
</script>
<style scoped>
#container {
  display: block;
  width: 1000px;
  height: 400px;
  margin: 0 auto;
  padding: 0;
  overflow: hidden;
}
</style>