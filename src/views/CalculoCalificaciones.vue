<template>
  <br><br>
  <form @submit.prevent="submitForm" class="container">
    <div class="form-group">
      <label for="nota1">Nota 1</label>
      <input type="number" v-model="nota1" min="10" max="70" class="form-control"/>
    </div>

    <div class="form-group">
      <label for="nota2">Nota 2</label>
      <input type="number" v-model="nota2" min="10" max="70" class="form-control"/>
    </div>

    <div class="form-group">
      <label for="nota3">Nota 3</label>
      <input type="number" v-model="nota3" min="10" max="70" class="form-control" />
    </div>

    <div class="form-group">
      <label for="asistencia">Asistencia (%):</label>
      <input type="number" v-model="asistencia" min="0" max="100" class="form-control"/>
    </div>

    <button @click="calcular" class="btn-primary">Calcular</button>

    <div v-if="mensajeError" class="error-message">
      <p>{{ mensajeError }}</p>
    </div>

    <div v-if="resultado !== null">
      <p>El promedio es: {{ promedioPonderado }}</p>
      <p>Tu estado es: {{ resultado }}</p>
    </div>
  </form>
</template>
<script>
export default {
  data() {
    return {
      nota1: null,
      nota2: null,
      nota3: null,
      asistencia: null,
      promedioPonderado: 0,
      resultado: null,
      mensajeError: '', 
    };
  },
  methods: {
    calcular() {
      if (this.validarCampos()) {
        const promedio = (this.nota1 * 0.35) + (this.nota2 * 0.35) + (this.nota3 * 0.30);
        this.promedioPonderado = promedio.toFixed(2);
        this.mensajeError = ''; 

        if (promedio >= 40 && this.asistencia >= 80) {
          this.resultado = "Aprobado";
        } else {
          this.resultado = "Reprobado";
        }
      } else {
        this.mensajeError = 'Por favor ingrese valores válidos.'; 
        this.resultado = null; 
      }
    },
    validarCampos() {
      return (
        this.nota1 >= 10 && this.nota1 <= 70 &&
        this.nota2 >= 10 && this.nota2 <= 70 &&
        this.nota3 >= 10 && this.nota3 <= 70 &&
        this.asistencia >= 0 && this.asistencia <= 100
      );
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
    text-align: center;
  }

  .form-group {
    margin-bottom: 20px;
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
    background-color: #007bff;
    color: #fff;
    padding: 10px 20px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }

  .error-message p {
    color: red; 
    font-weight: bold;
  }
</style>
