<template>
  <Layout>
    <PageHeader :title="title" :items="items" />
    <b-row class="main-container">
      <b-col>
        <b-tabs pills nav-wrapper-class="col-md-3 col-sm-3 col-4">
          <b-tab
            title="Empresa"
            @click="
              [
                (title = 'Cadastro de Empresa'),
                (items[1].text = 'Cadastro de Empresa'),
              ]
            "
          >
            <b-container fluid>
              <b-row class="mt-4 ml-1 mr-1">
                <label for="cnpj-empresa">CNPJ</label>
                <b-form-input
                  id="cnpj-empresa"
                  type="text"
                  v-model="mask.cnpjEmpresaMasked"
                  v-mask="'##.###.###/####-##'"
                ></b-form-input>
              </b-row>
              <b-row class="mt-4 ml-1 mr-1">
                <label for="fantasia">Nome Fantasia</label>
                <b-form-input
                  id="fantasia"
                  type="text"
                  v-model="novaEmpresa.nome_fantasia"
                ></b-form-input>
              </b-row>
              <b-row class="mt-4 ml-1 mr-1">
                <label for="razao-social-empresa">Razão Social</label>
                <b-form-input
                  id="razao-social-empresa"
                  type="text"
                  v-model="novaEmpresa.razao_social"
                ></b-form-input>
              </b-row>
              <b-row
                style="paddingTop:30px;paddingBottom:30px;"
                class="ml-1"
                align-v="center"
              >
                <b-button variant="primary" class="mr-3">Novo</b-button>
                <b-button @click="salvarEmpresa" variant="primary" class="mr-3"
                  >Confirmar</b-button
                >
                <b-button disabled variant="primary" class="mr-3"
                  >Cancelar</b-button
                >
                <b-button disabled variant="primary" class="mr-3"
                  >Excluir</b-button
                >
                <b-button variant="primary" class="mr-3">Sair</b-button>
                <i
                  class="fas fa-question-circle fa-2x ml-5"
                  style="color: #556ee6; cursor: pointer"
                  v-b-tooltip.hover
                  title="Help"
                  v-b-modal="'help-empresa'"
                ></i>
                <b-modal
                  id="help-empresa"
                  title="Cadastro de Empresa"
                  hide-footer
                >
                  <p>
                    Essa tela tem por objetivo o cadastro das empresas
                    autorizadas a operarem com o sistema de cadastro de produtos
                    da Bagarote. <br />
                    <br />
                    Não se trata de um cadastro de clientes, mas apenas das
                    empresas que terão acesso ao cadastro de produtos com o
                    único propósito de controle de acesso e rastreabilidade das
                    operações realizadas no sistema.
                  </p>
                </b-modal>
              </b-row>
            </b-container>
          </b-tab>
          <b-tab
            title="Loja Física"
            @click="
              [
                (title = 'Cadastro de Loja Física'),
                (items[1].text = 'Cadastro de Loja Física'),
              ]
            "
          >
            <b-container fluid>
              <b-row class="mt-4">
                <b-col>
                  <label for="empresa">Empresa</label>
                  <b-form-input
                    list="empresa"
                    @change="atribuirEmpresaLoja($event)"
                  ></b-form-input>
                  <datalist id="empresa">
                    <option
                      v-for="empresa in empresas"
                      :key="empresa.id_empresa"
                      :id="empresa.id_empresa"
                    >
                      {{ empresa.nome_fantasia }}
                    </option>
                  </datalist>
                </b-col>
                <b-col>
                  <label for="cnpj-loja-fisica">CNPJ</label>
                  <b-form-input
                    id="cnpj-loja-fisica"
                    type="text"
                    v-model="mask.cnpjLojaFisicaMasked"
                    v-mask="'##.###.###/####-##'"
                  ></b-form-input>
                </b-col>
              </b-row>
              <b-row class="mt-4 ml-1 mr-1">
                <label for="nome-loja">Nome da Loja</label>
                <b-form-input
                  id="nome-loja"
                  type="text"
                  v-model="novaLojaFisica.loja"
                ></b-form-input>
              </b-row>
              <b-row class="mt-4 ml-1 mr-1">
                <label for="endereco">Endereço</label>
                <b-form-input
                  id="endereco"
                  type="text"
                  v-model="novaLojaFisica.endereco_completo"
                ></b-form-input>
              </b-row>
              <b-row class="mt-4">
                <b-col>
                  <label for="contato">Contato</label>
                  <b-form-input
                    id="contato"
                    type="text"
                    v-model="novaLojaFisica.contato"
                  ></b-form-input>
                </b-col>
                <b-col>
                  <label for="celular">Celular</label>
                  <b-form-input
                    id="celular"
                    type="text"
                    v-model="mask.celLojaFisicaMasked"
                    v-mask="'(##)####-#####'"
                  ></b-form-input>
                </b-col>
              </b-row>
              <b-row class="mt-4">
                <b-col>
                  <label for="telefone">Telefone</label>
                  <b-form-input
                    id="telefone"
                    type="text"
                    v-model="mask.telLojaFisicaMasked"
                    v-mask="'(##)####-####'"
                  ></b-form-input>
                </b-col>
                <b-col>
                  <label for="whatsapp">Whatsapp</label>
                  <b-form-input
                    id="whatsapp"
                    type="text"
                    v-model="mask.whatsappLojaFisicaMasked"
                    v-mask="'(##)####-#####'"
                  ></b-form-input>
                </b-col>
              </b-row>
              <b-row
                style="paddingTop:30px;paddingBottom:30px;"
                class="ml-1"
                align-v="center"
              >
                <b-button variant="primary" class="mr-3">Novo</b-button>
                <b-button
                  @click="salvarLojaFisica"
                  variant="primary"
                  class="mr-3"
                  >Confirmar</b-button
                >
                <b-button disabled variant="primary" class="mr-3"
                  >Cancelar</b-button
                >
                <b-button disabled variant="primary" class="mr-3"
                  >Excluir</b-button
                >
                <b-button variant="primary" class="mr-3">Sair</b-button>
                <i
                  class="fas fa-question-circle fa-2x ml-5"
                  style="color: #556ee6; cursor: pointer"
                  v-b-tooltip.hover
                  title="Help"
                  v-b-modal="'help-loja-fisica'"
                ></i>
                <b-modal
                  id="help-loja-fisica"
                  title="Cadastro de Loja Física"
                  hide-footer
                >
                  <p>
                    Essa tela tem por objetivo o cadastro das lojas vinculadas a
                    um cliente/parceiro que envia produtos para fotografar em
                    nossos studios. <br />
                    <br />
                    Importante registrar o contato da pessoa responsável por
                    despachar/receber os produtos na loja para que possamos
                    resolver algum problema.
                  </p>
                </b-modal>
              </b-row>
            </b-container>
          </b-tab>
        </b-tabs>
      </b-col>
    </b-row>
  </Layout>
</template>

<script>
import Layout from "../../layouts/main";
import PageHeader from "@/components/page-header";

import { http } from "@/config/http/http";

export default {
  components: {
    Layout,
    PageHeader,
  },

  data() {
    return {
      title: "Cadastro de Empresas",
      items: [
        {
          text: "Home",
          href: "/",
        },
        {
          text: "Cadastro de Empresas",
          active: true,
        },
      ],
      mask: {
        cnpjEmpresaMasked: null,
        cnpjLojaFisicaMasked: null,
        celLojaFisicaMasked: null,
        telLojaFisicaMasked: null,
        whatsappLojaFisicaMasked: null,
      },

      empresas: [],
      novaEmpresa: {
        id_empresa: "",
        cnpj: null,
        nome_fantasia: null,
        razao_social: null,
      },
      novaLojaFisica: {
        id_loja_fisica: "",
        id_empresa: null,
        cnpj: null,
        loja: null,
        endereco_completo: null,
        contato: null,
        cel: null,
        tel: null,
        whatsapp: null,
      },
    };
  },

  created() {
    this.listarEmpresas();
  },

  methods: {
    listarEmpresas() {
      http.get("empresas").then((res) => {
        this.empresas = res.data;
        /* eslint-disable no-console */
        // console.log(this.empresas)
        /* eslint-enable no-console */
      });
    },

    salvarEmpresa() {
      this.novaEmpresa.cnpj = this.mask.cnpjEmpresaMasked.replace(
        /[^a-zA-Z0-9]/g,
        ""
      );

      http.post("empresa", this.novaEmpresa).then(() => {
        this.mask.cnpjEmpresaMasked = "";
        this.novaEmpresa = {};
        alert("Empresa cadastrada com sucesso!");
        this.listarEmpresas();
      });
    },

    salvarLojaFisica() {
      this.novaLojaFisica.cnpj = this.mask.cnpjLojaFisicaMasked.replace(
        /[^a-zA-Z0-9]/g,
        ""
      );
      this.novaLojaFisica.cel = this.mask.celLojaFisicaMasked.replace(
        /[^a-zA-Z0-9]/g,
        ""
      );
      this.novaLojaFisica.tel = this.mask.telLojaFisicaMasked.replace(
        /[^a-zA-Z0-9]/g,
        ""
      );
      this.novaLojaFisica.whatsapp = this.mask.whatsappLojaFisicaMasked.replace(
        /[^a-zA-Z0-9]/g,
        ""
      );

      http.post("loja-fisica", this.novaLojaFisica).then(() => {
        this.mask.cnpjLojaFisicaMasked = null;
        this.mask.celLojaFisicaMasked = null;
        this.mask.telLojaFisicaMasked = null;
        this.mask.whatsappLojaFisicaMasked = null;
        this.novaLojaFisica = {};
        alert("Loja física cadastrada com sucesso!");
      });
    },

    atribuirEmpresaLoja(event) {
      for (var empresa in this.empresas) {
        if (this.empresas[empresa].nome_fantasia == event) {
          this.novaLojaFisica.id_empresa = this.empresas[empresa].id_empresa;
        }
      }
    },
  },
};
</script>

<style scoped>
.btn {
  width: 100px;
}

@media (max-width: 720px) {
  .btn {
    display: block;
    width: 100%;
    margin-bottom: 10px;
  }
  .fa-question-circle {
    position: absolute;
    right: 30px;
    bottom: 5px;
  }
}
</style>