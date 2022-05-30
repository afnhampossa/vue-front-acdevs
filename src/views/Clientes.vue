<template>
  <div class="about">
    <div class="container">
      <div>
        <h2>
          <strong>
            GESTÃO DE CLIENTES
          </strong>
        </h2>
      </div>
      <hr>
      <!-- criar novo cliente -->
      <div class="d-flex">
        <button type="button" class="btn btn-outline-secondary" data-bs-toggle="modal" data-bs-target="#moalCadCliente">
          Novo Cliente
        </button>
      </div>
      <hr>
      <br>

      <!-- tabela de clientes -->
      <div class="row">
        <table class="table">
          <thead class="thead-dark">
            <tr>
              <th scope="col">#</th>
              <th scope="col">Nome</th>
              <th scope="col">E-mail</th>
              <th scope="col">Endereço</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(item, index) in clientes" :key="index">
              <th scope="row">{{(index + 1)}}</th>
              <td>{{item.nome}}</td>
              <td>{{item.email}}</td>
              <td>{{item.endereco}}</td>
            </tr>
          </tbody>
        </table>
      </div>

      <!-- Modal de cadastro de clientes -->
      <div class="modal fade" id="moalCadCliente" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
        <div class="modal-dialog" role="document">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title" id="exampleModalLabel"><strong>Cadastro de Cliente</strong></h5>
              <button type="button" class="close" data-bs-dismiss="modal" aria-label="Close">
                <span aria-hidden="true">&times;</span>
              </button>
            </div>
            <div class="modal-body">
              <form>
                <div class="form-group">
                  <label for="inputName" style="float: left;">Nome completo</label>
                  <input v-model="cliente.nome" type="text" class="form-control" id="inputName" placeholder="Ex: Angelino Fernando">
                </div>
                <div class="form-group">
                  <label for="inputEmail" style="float: left;">E-mail</label>
                  <input v-model="cliente.email" type="email" class="form-control" id="inputEmail" placeholder="Ex: angelino@gmail.com">
                </div>
                <div class="form-group">
                  <label for="inputEndereco" style="float: left;">Endereco</label>
                  <input v-model="cliente.endereco" type="text" class="form-control" id="inputEndereco" placeholder="Ex: Maputo, Avenida Eduardo Mondlane">
                </div>
              </form>
            </div>
            <div class="modal-footer">
              <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Cancelar</button>
              <button type="button" @click="cadCliente" class="btn btn-primary">Salvar</button>
            </div>
          </div>
        </div>
      </div>
    </div>

  </div>
</template>
<script>
import swal from 'sweetalert';

export default {
  name: 'Cliente',
  components: {
  },

  data(){
    return {
      cliente: {
        nome: '',
        email: '',
        endereco: ''
      },
      clientes:[],
    }
  },

  mounted(){
    this.clientes
  },

  methods: {

    cadCliente(){
      var cliente_ = {
        nome: this.cliente.nome,
        email: this.cliente.email,
        endereco: this.cliente.endereco
      }

      this.clientes.push(cliente_)

      swal("Sucesso!", "Cadastrado com sucesso!", "success");
    },
  }
}
</script>
