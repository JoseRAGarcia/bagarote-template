<template>
  <Layout>
    <b-row>
      <!-- Primeira coluna principal -->
      <b-col class="camera" cols="8">
        <!-- Tela da câmera -->
        <div id="canon">
          <div class="cam-config">
            <p>
              {{ camConfig.nome }},
              <span
                >Data:
                {{
                  camConfig.dataAtual.getDate() +
                  "/" +
                  camConfig.dataAtual.getMonth() +
                  "/" +
                  camConfig.dataAtual.getFullYear() +
                  " " +
                  camConfig.dataAtual.getHours() +
                  ":" +
                  camConfig.dataAtual.getMinutes()
                }}</span
              >
            </p>
            <p>Diafragma: {{ camConfig.diafragma }}</p>
            <p>ISO: {{ camConfig.iso }}</p>
            <p>WB: {{ camConfig.wb }}</p>
            <p>AF</p>
          </div>

          <div class="hl-1" :style="y1"></div>
          <div class="hl-2" :style="y2"></div>
          <div class="vl-1" :style="x1"></div>
          <div class="vl-2" :style="x2"></div>

          <!-- Controle das guias de centralização -->
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

        <!-- Área de botões -->
        <b-row class="row controles" id="main-ctrl" align-v="center">
          <b-col>
            <i
              v-b-tooltip.hover
              title="Girar para esquerda"
              class="fas fa-undo-alt fa-2x btn-ctrl"
            ></i>
          </b-col>
          <b-col>
            <i
              v-b-tooltip.hover
              title="Girar para direita"
              class="fas fa-redo-alt fa-2x btn-ctrl"
            ></i>
          </b-col>
          <b-col></b-col>
          <b-col>
            <i
              v-b-tooltip.hover
              title="Configurar câmera"
              class="fas fa-info-circle fa-2x btn-ctrl"
            ></i>
          </b-col>
          <b-col>
            <i
              v-b-tooltip.hover
              title="Focar"
              class="fa fa-crosshairs fa-2x btn-ctrl"
            ></i>
          </b-col>
          <b-col cols="4">
            <b-row class="text-center">
              <b-col>
                <i
                  v-b-tooltip.hover
                  title="Diminuir a velocidade do obturador"
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
                  v-b-tooltip.hover
                  title="Aumentar a velocidade do obturador"
                  class="fas fa-caret-right fa-4x"
                  id="aumenta-velocidade"
                  style="cursor: pointer"
                  @click="alterarVelocidadeObturador($event)"
                ></i>
              </b-col>
            </b-row>
          </b-col>
          <b-col>
            <i
              v-b-tooltip.hover
              title="Disparar"
              class="fas fa-camera fa-2x btn-ctrl"
            ></i>
          </b-col>
        </b-row>
      </b-col>

      <!-- Segunda coluna principal -->
      <b-col class="ml-4 sessao">
        <center>
          <!-- Área de entrada do GTIN -->
          <form class="form-horizontal" role="form">
            <b-row align-v="center">
              <b-col cols="10">
                <b-form-group
                  id="example-search"
                  label-cols-sm="2"
                  label-cols-lg="2"
                  label="GTIN"
                  label-for="gtin"
                >
                  <b-form-input id="gtin" value="" type="search" name="search" v-model="produto.gtin">                                    
                  </b-form-input>                  
                </b-form-group>                
              </b-col>
              <b-col>
                <i v-if="produto.gtin==''" class="fas fa-barcode fa-2x"></i>
                <i v-else-if="produto.gtin=='1111111111111'" class="fas fa-exclamation-triangle fa-2x" style="color: red"></i>                
                <i v-else-if="produto.gtin=='2222222222222'" class="fas fa-check-circle fa-2x" style="color: green"></i>
                <b-spinner v-else small class="spinner" variant="primary" key="primary"></b-spinner>                
              </b-col>
            </b-row>
          </form>
          <!-- Área com a descrição do produto -->
          <textarea
            class="form-control form-control text-center"
            style="resize: none; margin-top: 4px"
            name="Text1"
            cols="40"
            rows="3"
            readonly
          >
Lorem ipsum, dolor sit amet consectetur adipisicing elit. Inventore corporis enim a itaque impedit cupiditate perferendis eaque numquam non obcaecati.</textarea
          >
          <!-- Área com as imagens do produto -->
          
          <!-- <b-row class="mt-1" style="height:400px; paddingTop:10%; paddingBottom:10%; overflow:auto;">
            <b-col>
              <div class="product-detai-imgs">
                <b-tabs pills vertical end nav-wrapper-class="col-md-3 col-sm-3 col-4">
                  <b-tab>
                    <template v-slot:title>
                      <img src="@/assets/images/sessao-fotografica/nescau_1.png" alt="" class="img-fluid mx-auto d-block tab-img rounded">
                    </template>
                    <div class="product-img">
                      <img src="@/assets/images/sessao-fotografica/nescau_1.png" alt="" class="img-fluid mx-auto d-block">
                    </div>
                  </b-tab>

                  <b-tab>
                    <template v-slot:title>
                      <img src="@/assets/images/sessao-fotografica/nescau_2.png" alt="" class="img-fluid mx-auto d-block tab-img rounded">
                    </template>
                    <div class="product-img">
                      <img src="@/assets/images/sessao-fotografica/nescau_2.png" alt="" class="img-fluid mx-auto d-block">
                    </div>
                  </b-tab>

                  <b-tab>
                    <template v-slot:title>
                      <img src="@/assets/images/sessao-fotografica/nescau_3.png" alt="" class="img-fluid mx-auto d-block tab-img rounded">
                    </template>
                    <div>
                      <img src="@/assets/images/sessao-fotografica/nescau_3.png" alt="" class="img-fluid mx-auto d-block">
                    </div>
                  </b-tab>

                  <b-tab>
                    <template v-slot:title>
                      <img src="@/assets/images/sessao-fotografica/nescau_1.png" alt="" class="img-fluid mx-auto d-block tab-img rounded">
                    </template>
                    <div>
                      <img src="@/assets/images/sessao-fotografica/nescau_1.png" alt="" class="img-fluid mx-auto d-block">
                    </div>
                  </b-tab>                  
                </b-tabs>
              </div>
            </b-col>
          </b-row>           -->
          <b-row class="bd-img">
            <b-col cols="5">
              <img :src="produto.imagens[mainImage]" alt="" id="img-main" />
            </b-col>
            <b-col cols="2" class="imagem-sm overflow-auto">
              <b-row v-for="(img, index) in produto.imagens" :key="index" @click="alterarImagem($event)">
                <img
                  :id="index"
                  class="img-sm"
                  :src="produto.imagens[index]"
                  alt=""
                />
              </b-row>
            </b-col>
          </b-row>
          <!-- Área de botões -->
          <b-row class="controles" id="sec-ctrl" align-v="center">
            <b-col></b-col>
            <b-col>
              <i
                v-b-tooltip.hover
                title="Excluir"
                class="far fa-trash-alt fa-2x btn-ctrl"
              ></i>
            </b-col>
            <b-col>
              <i
                v-b-tooltip.hover
                title="Fotografar sem GTIN"
                class="fas fa-ban fa-4x"
                style="position: absolute; cursor: pointer"
              ></i>
              <i class="fas fa-barcode fa-2x btn-ctrl"></i>
            </b-col>
            <b-col>
              <i
                v-b-tooltip.hover
                title="Pesquisar no Google"
                class="fab fa-google-plus fa-2x btn-ctrl"
              >
              </i>
            </b-col>
            <b-col>
              <i
                v-b-tooltip.hover
                title="Sair"
                class="fas fa-sign-out-alt fa-2x btn-ctrl"
              ></i>
            </b-col>
          </b-row>
        </center>
      </b-col>
    </b-row>
  </Layout>
</template>

<script>
import Layout from '../../layouts/main'

export default {
  components: {
    Layout,
  },

  data() {
    return {
      mainImage: 0,
      xValue: 0,
      yValue: 0,
      velObiturador: 1,
      produto: {
        gtin: '',
        nome: '',
        descricao: '',
        imagens: [
          require("@/assets/images/sessao-fotografica/nescau_1.png"),
          require("@/assets/images/sessao-fotografica/nescau_2.png"),
          require("@/assets/images/sessao-fotografica/nescau_3.png"),
          require("@/assets/images/sessao-fotografica/nescau_4.png"),
          require("@/assets/images/sessao-fotografica/nescau_5.png"),
          require("@/assets/images/sessao-fotografica/nescau_6.png")    
          ]
      },
      camConfig: {
        nome: "Wander",
        diafragma: "F8.0",
        iso: 100,
        wb: 0.0,
        dataAtual: new Date(),
      },
    };
  },

  methods: {
    alterarImagem(event) {
      this.mainImage = event.target.id
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
.cam-config {
  color: #fff;
  position: absolute;
  padding: 5px;
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
.sessao {
  margin: 10px 0 0 10px;
  width: 100%;
  height: 100vh;
}
#nome-produto {
  width: 100%;
}
#img-main {
  width: 100%;
}
.img-sm {
  height: 100px;
  width: 100px;
  cursor: pointer;
}
.imagem-sm {
  height: 300px;
}
.bd-img {
  padding: 45px 0 27px 0;
  margin: 10px 0 0 0;
  width: 200%;
}
.controles {
  position: absolute;
  bottom: 10%;
  width: 100%;
  height: 80px;
  margin: 10px 0 0 0;
  padding: 10px;
  border-radius: 5px;
  background-color: #e9ecef;
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
}
.vl-2 {
  border-right: 3px dotted #f8f8fb;
  height: 100%;
  position: relative;
  left: 0;
}
.hl-1 {
  border-bottom: 3px dotted #f8f8fb;
  height: 100%;
  width: 100%;
  position: absolute;
  top: -100%;
  float: left;
}
.hl-2 {
  border-bottom: 3px dotted #f8f8fb;
  height: 100%;
  width: 100%;
  position: absolute;
  top: 0;
  float: left;
}
</style>