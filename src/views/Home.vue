<template>
  <v-container fluid>
    <v-layout row wrap align-center justify-space-around>
      <v-flex xs12 md5 class="grey lighten-2 pa-2 mb-2">
        <v-card
          id="wavecontrollerWrap"
          ref="wavecontrollerWrapRef"
          class="pa-2"
        >
          <!-- . -->
        </v-card>
        <v-card v-if="status" class="my-2">
          <v-card-text class="subheading">
            <p color="info">
              {{ status }}
            </p>
          </v-card-text>
        </v-card>
      </v-flex>

      <v-flex xs12 md5 class="pa-1">
        <v-card flat class="pa-3" id="canvasWrap" ref="canvasWrapRef">
          <canvas id="canvasKibWave" ref="canvasKibWaveRef"></canvas>
        </v-card>
      </v-flex>

      <v-flex xs12 class="my-2">
        <v-card>
          <v-card-title>
            <h3 class="title">Credits</h3>
          </v-card-title>
          <v-card-text>
            <p>
              This project has been forked from Njeri. More modifications to be
              updated later.
            </p>
          </v-card-text>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
/* eslint-disable no-console */
/* eslint-disable no-unused-vars */

let SELF;
import * as dat from "dat.gui";

export default {
  name: "",
  components: {},
  props: {},
  data() {
    return {
      status: "",
      properties: {
        wave: {
          // y: canvas.height / 2,
          y: 0,
          length: 0.01,
          amplitude: 100,
          frequency: 0.01
        },
        strokeColor: {
          h: 200,
          s: 50,
          l: 50
        },
        backgroundColor: {
          r: 255,
          g: 255,
          b: 255,
          a: 1
        }
      }
    };
  },
  methods: {
    // .
  },
  computed: {},
  watch: {},
  beforeCreate() {
    SELF = this;
  },
  created() {},
  mounted() {
    SELF.$nextTick(() => {
      let gui = new dat.GUI({ autoPlace: false });

      let customContainer = document.getElementById("wavecontrollerWrap");
      customContainer.appendChild(gui.domElement);
      // console.log(gui.domElement);

      let kibcanvas = document.querySelector("canvas");
      let c = kibcanvas.getContext("2d");

      kibcanvas.width = 400; // innerWidth
      kibcanvas.height = 300; // innerHeight
      // SELF.status = `height[ ${kibcanvas.height} ], width[ ${
      //   kibcanvas.width
      // } ]`;
      SELF.properties.wave.y = kibcanvas.height / 2;

      let waveFolder = gui.addFolder("wave");
      waveFolder.add(SELF.properties.wave, "y", 0, kibcanvas.height);
      waveFolder.add(SELF.properties.wave, "length", -0.01, 0.01);
      waveFolder.add(SELF.properties.wave, "amplitude", -300, 300);
      waveFolder.add(SELF.properties.wave, "frequency", -0.01, 1);

      let strokeFolder = gui.addFolder("stroke");
      strokeFolder.add(SELF.properties.strokeColor, "h", 0, 255);
      strokeFolder.add(SELF.properties.strokeColor, "s", 0, 100);
      strokeFolder.add(SELF.properties.strokeColor, "l", 0, 100);

      let backgroundColorFolder = gui.addFolder("background");
      backgroundColorFolder.add(SELF.properties.backgroundColor, "r", 0, 255);
      backgroundColorFolder.add(SELF.properties.backgroundColor, "g", 0, 255);
      backgroundColorFolder.add(SELF.properties.backgroundColor, "b", 0, 255);
      backgroundColorFolder.add(SELF.properties.backgroundColor, "a", 0, 1);

      let increment = SELF.properties.wave.frequency;

      function animate() {
        requestAnimationFrame(animate);
        c.fillStyle = `rgba(${SELF.properties.backgroundColor.r}, ${
          SELF.properties.backgroundColor.g
        }, ${SELF.properties.backgroundColor.b}, ${
          SELF.properties.backgroundColor.a
        })`;
        // c.fillStyle = `rgba(255,255,255,1)`;

        // c.rect(0, 0, kibcanvaswrapheight, 300);
        // c.stroke();
        c.fillRect(0, 0, kibcanvas.width, kibcanvas.height);
        c.beginPath();

        c.moveTo(0, kibcanvas.height / 2);

        for (var i = 0; i < kibcanvas.width; i++) {
          c.lineTo(
            i,
            SELF.properties.wave.y +
              Math.sin(i * SELF.properties.wave.length + increment) *
                SELF.properties.wave.amplitude *
                Math.sin(increment)
          );
        }

        c.strokeStyle = `hsl(${Math.abs(
          SELF.properties.strokeColor.h * Math.sin(increment)
        )}, ${SELF.properties.strokeColor.s}%, ${
          SELF.properties.strokeColor.l
        }%)`;
        c.stroke();
        increment += SELF.properties.wave.frequency;
      } // end-animate()

      animate();
    });
  }
};
</script>

<style scoped>
#wavecontrollerWrap {
  /*overflow: hidden;*/
  height: 250px;
  z-index: 1;
  background-color: rgba(255, 255, 255, 0.1);
}
#canvasWrap {
  /*overflow: auto;*/
  background-color: rgba(255, 255, 255, 0.1);
}
</style>
