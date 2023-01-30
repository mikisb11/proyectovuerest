<template>
  <div id="tabla-usuarios">
    <div v-if="!usuarios.length" class="alert alert-info" role="alert">
      No existen usuarios
    </div>
    <table class="table">
      <thead>
      <tr>
        <th>IdUser</th>
        <th>Usuario</th>
        <th>Nombre</th>
        <th>Email</th>
        <th>Ciudad</th>
        <th>Teléfono</th>
        <th colspan="2">OPERACIONES</th>
      </tr>
      </thead>
      <tbody>
        <tr v-for="usuario in usuarios" :key="usuario.id">
         <td v-if="editando  === usuario.id">
           <label>{{ usuario.id }} </label>
          </td>
          <td v-else>
             {{ usuario.id }}
          </td>
          <td v-if = "editando === usuario.id">
            <input type="text" class = "form-control" v-model="usuario.name" />
          </td>
          <td v-else>
            {{ usuario.name }}
          </td>
          <td v-if = "editando === usuario.id">
            <input type="text" class = "form-control" v-model="usuario.username" />
          </td>
          <td v-else>
            {{ usuario.username }}
          </td>
          <td v-if = "editando === usuario.id">
            <input type="text" class = "form-control" v-model="usuario.email" />
          </td>
          <td v-else>
            {{ usuario.email }}
          </td>
          <td v-if = "editando === usuario.id">
            <input type="text" class = "form-control" v-model="usuario.city" />
          </td>
          <td v-else>
            {{ usuario.city }}
          </td>
          <td v-if = "editando === usuario.id">
            <input type="text" class = "form-control" v-model="usuario.phone" />
          </td>
          <td v-else>
             {{ usuario.phone }}
          </td>
          <td v-if = "editando === usuario.id"><th>
            <button class = 'btn btn-success btn-sm' @click="actualizarusuario(usuario)" > 💾 Guardar</button>
            </th>
            <th>
            <button class = 'btn btn-secondary btn-sm' @click="cancelaredicion(usuario)">❌Cancelar</button>
            </th>
          </td>
          <td v-else><th>
            <button class = 'btn btn-info btn-sm' @click ="editarusuario(usuario)">✏️  Editar </button>
           </th> <th>
          <button class = 'btn btn-danger btn-sm' @click="$emit('eliminarusuario', usuario)">🗑️ Eliminar</button>
             </th>
          </td>
        </tr>
      </tbody>
    </table>
  </div>

</template>

<script>
export default {
  props:{
    usuarios: Array,
  },
  data(){
    return{
      editando: null,
    }
  },
  methods:{
    editarusuario(usuario){
      this.usuarioEditado = Object.assign({}, usuario);
      this.editando = usuario.id;
    },
    cancelaredicion(usuario){
      Object.assign(usuario, this.usuarioEditado);
      this.editando = null;
    },
    actualizarusuario(usuario){
      if (!usuario.name.length || !usuario.username.length || !usuario.email.length || !usuario.city.length || !usuario.phone.length ) {
        return;
      }
      this.$emit('actualizarusuario', usuario);
      this.editando = null
    }
  }
}
</script>

<style scoped>
  *{
    color: white;
  }
</style>