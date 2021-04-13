<template>
  <Layout>
    <b-container>
      <b-row>
        <b-col class="camera" cols="8">
          <div id="canon">
            <div class="hl-1" :style="y1"></div>
            <div class="hl-2" :style="y2"></div>
            <div class="vl-1" :style="x1"></div>
            <div class="vl-2" :style="x2"></div>

            <input
              type="range"
              min="0"
              max="50"
              value="0"
              class="form-control-range horizontal-slider"
              v-model="xValue"
            />
            <input
              type="range"
              min="1"
              max="50"
              value="0"
              class="form-control-range vertical-slider"
              v-model="yValue"
            />
          </div>
          <b-row class="row controles" id="main-ctrl">
            <b-col>
              <i class="fas fa-undo-alt fa-2x btn-ctrl"></i>
            </b-col>
            <b-col>
              <i class="fas fa-redo-alt fa-2x btn-ctrl"></i>
            </b-col>
            <b-col></b-col>
            <b-col>
              <i class="fas fa-info-circle fa-2x btn-ctrl"></i>
            </b-col>
            <b-col>
              <i class="fa fa-crosshairs fa-2x btn-ctrl"></i>
            </b-col>
            <b-col cols="4">
              <b-row class="text-center">
                <b-col>
                  <i
                    class="fas fa-caret-left fa-4x"
                    id="diminui-velocidade"
                    style="cursor: pointer"
                    @click="alterarVelocidadeObturador($event)"
                  ></i>
                </b-col>
                <b-col cols="7">
                  <input
                    type="text"
                    readonly
                    class="form-control text-center"
                    id="vel-obturador"
                    style="font-size: 28px"
                    :value="velObiturador + '/10'"
                  />
                </b-col>
                <b-col>
                  <i
                    class="fas fa-caret-right fa-4x"
                    id="aumenta-velocidade"
                    style="cursor: pointer"
                    @click="alterarVelocidadeObturador($event)"
                  ></i>
                </b-col>
              </b-row>
            </b-col>
            <b-col>
              <i class="fas fa-camera fa-2x btn-ctrl"></i>
            </b-col>
          </b-row>
        </b-col>
        <b-col class="ml-4">
          <b-form-group
            id="example-search"
            label-cols-sm="2"
            label-cols-lg="2"
            label="GTIN"
            label-for="gtin"
          >
            <b-form-input
              id="gtin"
              value=""
              type="search"
              name="search"
            ></b-form-input>
          </b-form-group>
        </b-col>
      </b-row>
    </b-container>
  </Layout>
</template>

<script>
import Layout from "../../layouts/main";

export default {
  components: {
    Layout,
  },

  data() {
    return {
      mainImage: require("@/assets/images/sessao-fotografica/nescau_1.png"),
      xValue: 0,
      yValue: 0,
      velObiturador: 1,
    };
  },

  methods: {
    alterarImagem(event) {
      this.mainImage = event.target.src;
    },
    alterarVelocidadeObturador(event) {
      if (event.target.id == "diminui-velocidade") {
        this.velObiturador--;
        if (this.velObiturador <= 1) {
          this.velObiturador = 1;
        }
      } else {
        this.velObiturador++;
        if (this.velObiturador >= 10) {
          this.velObiturador = 10;
        }
      }
    },
  },

  computed: {
    x1() {
      return `transform: translateX(${this.xValue}%)`;
    },

    x2() {
      return `transform: translateX(-${this.xValue}%)`;
    },

    y1() {
      return `transform: translateY(${this.yValue}%)`;
    },

    y2() {
      return `transform: translateY(-${this.yValue}%)`;
    },
  },
};
</script>

<style lang="scss" scoped>
* {
  margin: 0;
  padding: 0;
  list-style: none;
  text-decoration: none;
  box-sizing: border-box;
}

#canon {
  height: 75vh;
  width: 100%;
  background: url(../../../assets/images/sessao-fotografica/nescau.png)
    no-repeat left top;
  background-size: cover;
  position: relative;
  display: inline-block;
}
.horizontal-slider {
  width: 50%;
  position: relative;
  left: 50%;
  transform: rotate(-180deg);
}
.vertical-slider {
  width: 250px;
  float: right;
  transform: rotate(-90deg);
  position: absolute;
  left: calc(100% - 110px);
  top: calc(100% - 140px);
}

.controles {
  height: 80px;
  margin: 10px 0 0 0;
  padding: 10px;
  border-radius: 5px;
  background-color: #e9ecef;
}

#main-ctrl {
  width: 100%;
}

.btn-ctrl {
  border: 2px solid #2c3e50;
  border-radius: 50%;
  padding: 10px;
  background-color: #fff;
  cursor: pointer;
}

#vel-obturador {
  width: 100%;
  background-color: #fff;
}
.vl-1 {
  border-right: 3px dotted #f8f8fb;
  height: 100%;
  width: 100%;
  position: relative;
  left: -100%;
  float: left;
  /* background-color: #2c3e50; */
}
.vl-2 {
  border-right: 3px dotted #f8f8fb;
  height: 100%;
  position: relative;
  left: 0;
  /* background-color: #2c3e50; */
}
.hl-1 {
  border-bottom: 3px dotted #f8f8fb;
  height: 100%;
  width: 100%;
  position: absolute;
  top: -100%;
  float: left;
  /* background-color: #2c3e50; */
}
.hl-2 {
  border-bottom: 3px dotted #f8f8fb;
  height: 100%;
  width: 100%;
  position: absolute;
  top: 0;
  float: left;
  /* background-color: #2c3e50; */
}
</style>