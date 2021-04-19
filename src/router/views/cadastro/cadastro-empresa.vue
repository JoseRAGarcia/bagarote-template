<template>
  <Layout>
    <PageHeader :title="title" :items="items" />
    <b-row>
        <b-col>
            <b-tabs pills nav-wrapper-class="col-md-3 col-sm-3 col-4">
                <b-tab title="Empresa">
                    <b-container fluid>
                        <b-row class="mt-4">                  
                            <label for="cnpj">CNPJ</label>
                            <b-form-input id="cnpj" type="text"></b-form-input>                             
                        </b-row>
                        <b-row class="mt-4">                            
                            <label for="fantasia">Nome Fantasia</label>
                            <b-form-input id="fantasia" type="text"></b-form-input>                             
                        </b-row>
                        <b-row class="mt-4">                            
                            <label for="razaoSocial">Razão Social</label>
                            <b-form-input id="razaoSocial" type="text"></b-form-input>                             
                        </b-row>
                        <b-row style="paddingTop:30px;paddingBottom:30px;" align-v="center">
                            <b-button variant="primary" class="mr-3" style="width: 100px">Novo</b-button>
                            <b-button disabled variant="primary" class="mr-3" style="width: 100px">Confirmar</b-button>
                            <b-button disabled variant="primary" class="mr-3" style="width: 100px">Cancelar</b-button>
                            <b-button disabled variant="primary" class="mr-3" style="width: 100px">Excluir</b-button>
                            <b-button variant="primary"  style="width: 100px">Sair</b-button>
                            <i class="fas fa-question-circle fa-2x ml-5" style="color:#556ee6;cursor:pointer"></i>
                        </b-row>
                    </b-container>                    
                </b-tab>
                <b-tab title="Loja Física">
                    <b-container fluid>
                        <b-row class="mt-4">                           
                            <label for="empresa">Empresa</label>
                            <b-form-input list="empresa"></b-form-input>
                            <datalist id="empresa">
                                <option value="Empresa 1"></option>
                                <option value="Empresa 2"></option>
                            </datalist>                          
                        </b-row>
                        <b-row class="mt-4">                           
                            <label for="cnpj">CNPJ</label>
                            <b-form-input id="cnpj" type="text"></b-form-input>                             
                        </b-row>
                        <b-row class="mt-4">                            
                            <label for="nomeLoja">Nome da Loja</label>
                            <b-form-input id="nomeLoja" type="text"></b-form-input>                             
                        </b-row>
                        <b-row class="mt-4">                            
                            <label for="endereco">Endereço</label>
                            <b-form-input id="endereco" type="text"></b-form-input>                             
                        </b-row>
                        <b-row class="mt-4">                            
                            <label for="contato">Contato</label>
                            <b-form-input id="contato" type="text"></b-form-input>                             
                        </b-row>
                        <b-row class="mt-4">                            
                            <label for="celular">Celular</label>
                            <b-form-input id="celular" type="text"></b-form-input>                             
                        </b-row>
                        <b-row class="mt-4">                            
                            <label for="telefone">Telefone</label>
                            <b-form-input id="telefone" type="text"></b-form-input>                             
                        </b-row>
                        <b-row class="mt-4">                            
                            <label for="whatsapp">Whatsapp</label>
                            <b-form-input id="whatsapp" type="text"></b-form-input>                             
                        </b-row>
                        <b-row style="paddingTop:30px;paddingBottom:30px;" align-v="center">
                            <b-button variant="primary" class="mr-3" style="width: 100px">Novo</b-button>
                            <b-button disabled variant="primary" class="mr-3" style="width: 100px">Confirmar</b-button>
                            <b-button disabled variant="primary" class="mr-3" style="width: 100px">Cancelar</b-button>
                            <b-button disabled variant="primary" class="mr-3" style="width: 100px">Excluir</b-button>
                            <b-button variant="primary"  style="width: 100px">Sair</b-button>
                            <i class="fas fa-question-circle fa-2x ml-5" style="color:#556ee6;cursor:pointer"></i>
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
    };
  },
};
</script>

<style>
</style>