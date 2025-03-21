<template>
  <h1>Ingresar</h1>
  <label for="">Ingrese Correo</label>
  <input type="text" v-model="credenciales.email" />
  {{ errors.email }}
  <br />
  <label for="">Ingrese Contraseña</label>
  <input type="password" v-model="credenciales.password" />
  {{ errors.password }}
  <br />
  <button @click="funIngresar()">Ingresar</button>
  <br />
  {{ credenciales }}
  <br />
  {{ respuesta }}
</template>

<script setup>
import authService from "@/services/auth.service";
import { ref } from "vue";
import { useRouter } from "vue-router";

const credenciales = ref({
  email: "",
  password: "",
});
const respuesta = ref();
const errors = ref({});
const router = useRouter();

async function funIngresar() {
  errors.value = {};
  try {
    const res = await authService.login(credenciales.value);

    respuesta.value = res.data;

    localStorage.setItem("token", res.data.token);

    // redireccionar a la ruta de perfil
    router.push({ name: "perfil" });
  } catch (error) {
    errors.value = error.response?.data.errors;
  }
}
</script>
