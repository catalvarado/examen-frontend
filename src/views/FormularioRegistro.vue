<template>
 <br><br>
    <form @submit.prevent="submitForm" class="container">
    <div class="form-group">
      <label for="nombre">Nombre:</label>
      <input type="text" v-model="nombre" class="form-control"/>
    </div>

    <div class="form-group">
      <label for="correo">Correo:</label>
      <input type="email" v-model="correo" class="form-control"/>
    </div>

    <div class="form-group">
      <label for="password">Contraseña:</label>
      <input type="password" v-model="password" class="form-control"/>
    </div>

    <div class="form-group">
      <label for="repeatPassword">Repetir Contraseña:</label>
      <input type="password" v-model="repeatPassword"  class="form-control"/>
    </div>

    <button @click="validarFormulario" class="btn-primary">Enviar</button>
 </form>
</template>

<script>
export default {
  data() {
    return {
      nombre: '',
      correo: '',
      password: '',
      repeatPassword: '',
    };
  },
  methods: {
    validarFormulario() {
      if (this.nombre === '') {
        alert('El campo Nombre es obligatorio.');
        return;
      }

      const correoRegex = /^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,6}$/;
      if (!correoRegex.test(this.correo)) {
        alert('Por favor ingrese un correo electrónico válido.');
        return;
      }

      if (this.password === '' || this.repeatPassword === '') {
        alert('Debe completar ambos campos de contraseña.');
        return;
      }

      if (this.password !== this.repeatPassword) {
        alert('Las contraseñas no coinciden.');
        return;
      }

      alert('El registro se ha realizado correctamente');
    },
  },
};
</script>

<style scoped>
  .container {
        width: 70%;
        margin: 0 auto;
        padding: 20px;
        border: 1px solid #ccc;
        border-radius: 5px;
        
    }

    .form-group {
        margin-bottom: 20px;
        text-align: center;
    }

    .label {
        font-weight: bold;
    }

    .form-control {
        width: 100%;
        padding: 10px;
        border: 1px solid #ccc;
        border-radius: 5px;
        box-sizing: border-box;
    }
    .btn-primary {
        background-color: #00cc33;
        color: #fff;
        padding: 10px 20px;
        border: none;
        border-radius: 5px;
        cursor: pointer;
       }
       .container form {
    text-align: left;
    }
</style>
