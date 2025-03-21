<template>
  <h1>Usuarios</h1>
  <table>
    <thead>
      <tr>
        <th>Nombre</th>
        <th>Correo</th>
        <th>Acciones</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="usuario in usuarios" :key="usuario.id">
        <td>{{ usuario.name }}</td>
        <td>{{ usuario.email }}</td>
        <td>
          <router-link
            :to="{ name: 'editarUsuario', params: { id: usuario.id } }"
            >Editar</router-link
          >
          <button @click="funEliminar(usuario.id)">Eliminar</button>
        </td>
      </tr>
    </tbody>
  </table>
</template>
