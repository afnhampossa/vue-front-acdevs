<template>
  <div class="about">
    <div class="container">
      <div>
        <h2>
          <strong>
            GESTÃO DE CLIENTES ({{clientes.length}})
          </strong>
        </h2>
      </div>
      <hr>
      <!-- criar novo cliente -->
      <div class="d-flex">
        
      </div>
      <div class="row">
        <div class="col-6">
          <div class="col-auto">
            <label class="sr-only" for="inlineFormInputGroup">Pesquisar</label>
            <div class="input-group mb-2">
              <div class="input-group-prepend">
                <div class="input-group-text" @click="getUserSearch">
                  <i  id="inlineFormInputGroup" class="form-control fa fa-search"></i>
                </div>
              </div>
              <input type="text" v-model="search" class="form-control" id="inlineFormInputGroup" placeholder="Usuário">
            </div>
          </div>
        </div>
        <div class="col-6">
          <button type="button" class="btn btn-outline-secondary" data-bs-toggle="modal" data-bs-target="#moalCadCliente">
            Novo Cliente
          </button>
        </div>
      </div>
      <hr>
      <br>

      <!-- tabela de clientes -->
      <div class="row">
        <div class="alert alert-danger" role="alert" v-if="!hasDatas">
          Sem dados por mostrar
        </div>
        <table class="table" v-else>
          <thead class="thead-dark">
            <tr>
              <th scope="col">#</th>
              <th scope="col">Nome</th>
              <th scope="col">E-mail</th>
              <th scope="col">Endereço</th>
              <th scope="col">Operações</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(item, index) in clientes" :key="index">
              <th scope="row">{{(index + 1)}}</th>
              <td>{{item.nome}}</td>
              <td>{{item.email}}</td>
              <td>{{item.endereco}}</td>
              <td>
                <button type="button" @click="getUser(item.id)" data-bs-toggle="modal" data-bs-target="#moalEditCliente" class="btn btn-outline-primary"> <i class="fa fa-edit"></i></button>
                <button type="button" @click="getUser(item.id)" data-bs-toggle="modal" data-bs-target="#moalDeleteCliente" class="btn btn-outline-danger" style="margin-left:10px"><i class="fa fa-trash"></i></button>
              </td>
            </tr>
          </tbody>
        </table>
        <nav aria-label="Page navigation example">
          <ul class="pagination">
            <li class="page-item"><a class="page-link" href="#">Previous</a></li>
            <li class="page-item"><a class="page-link" href="#">1</a></li>
            <li class="page-item"><a class="page-link" href="#">2</a></li>
            <li class="page-item"><a class="page-link" href="#">3</a></li>
            <li class="page-item"><a class="page-link" href="#">Next</a></li>
          </ul>
        </nav>
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

      <!-- Modal de Editar de clientes -->
      <div class="modal fade" id="moalEditCliente" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
        <div class="modal-dialog" role="document">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title" id="exampleModalLabel"><strong>Edição de Cliente</strong></h5>
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
              <button type="button" @click="editCliente" class="btn btn-primary">Editar</button>
            </div>
          </div>
        </div>
      </div>

      <!-- Modal de Eliminação de clientes -->
      <div class="modal fade" id="moalDeleteCliente" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
        <div class="modal-dialog" role="document">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title" id="exampleModalLabel"><strong>Deseja eliminar {{cliente.nome}}?</strong></h5>
              <button type="button" class="close" data-bs-dismiss="modal" aria-label="Close">
                <span aria-hidden="true">&times;</span>
              </button>
            </div>
            <div class="modal-body">
              <p>Todos os dados serão perdidos.</p>
            </div>
            <div class="modal-footer">
              <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Cancelar</button>
              <button type="button" @click="deleteCliente" class="btn btn-primary">Eliminar</button>
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

  watch: {
    search: function () {
      this.axios.get(`http://localhost:5000/users-search/${this.search}`, 
        {
          headers: {
            'Content-Type': 'application/json',
          },
        }
      )
        .then(response => {
          this.clientes = response.data.data
        })
        .catch(error => {
          console.log(error)
        })
    }
  },

  computed: {
    hasDatas : function(){
      return this.clientes.length > 0
    }
  },

  data(){
    return {
      cliente: {
        nome: '',
        email: '',
        endereco: ''
      },
      clientes:[],
      totalClientes:0,
      search:''
    }
  },

  mounted(){
    this.getUsers()
  },

  methods: {

    getUsers() {
      this.axios.get("http://localhost:5000/users", 
        {
          headers: {
            'Content-Type': 'application/json',
          },
        }
      ).then((response) => {
        this.clientes = response.data.list
      })
    },

    getUser(id) {
      this.axios.get(`http://localhost:5000/users/${id}`, 
        {
          headers: {
            'Content-Type': 'application/json',
          },
        }
      ).then((response) => {
        this.cliente = response.data.data
      })
    },

    getUserSearch() {
      console.log('Clicado')
      
      this.axios.get(`http://localhost:5000/users-search/${this.search}`, 
        {
          headers: {
            'Content-Type': 'application/json',
          },
        }
      ).then((response) => {
        this.clientes = response.data.data
      })
    },


    cadCliente(){
      var cliente_ = {
        "nome": this.cliente.nome,
        "sexo_id": 1,
        "endereco": this.cliente.endereco,
        "email": this.cliente.email,
        "estado_id": 1
      }

      this.axios.post('http://localhost:5000/users', cliente_
      ).then((response) => {
          if(response.data.error === "")
          swal("Sucesso!", "Cadastrado com sucesso!", "success");
          this.getUsers()
      
      })
      
    },

    editCliente(){

      var cliente_ = {
        "nome": this.cliente.nome,
        "sexo_id": 1,
        "endereco": this.cliente.endereco,
        "email": this.cliente.email,
        "estado_id": 1
      }

      this.axios.put('http://localhost:5000/users/'+ this.cliente.id, cliente_
      ).then((response) => {
          if(response.data.error === "")
          swal("Sucesso!", "Atualizado com sucesso!", "success");
          this.getUsers()
      
      })
      
    },

     deleteCliente(){

      this.axios.delete('http://localhost:5000/users/'+ this.cliente.id
      ).then((response) => {
          if(response.data.error === "")
          swal("Sucesso!", "Eliminado com sucesso!", "success");
          this.getUsers()
      
      })
      
    },
  }
}
</script>
