<template>
  <div class="container mt-5">
    <div class="text-center">
      <h1 class="display-4 mb-4">Bienvenido a la Aplicación de Tareas con Vue</h1>
      <p class="lead mb-4">
        Gestiona tus tareas de manera eficiente, añadiendo nuevas tareas manualmente o extrayéndolas desde una API.
      </p>
      <img src="@/assets/logo.png" class="img-fluid mb-4 logo" alt="Vue logo" />
      <h2 class="mt-4">Secciones de la Aplicación</h2>
      <p class="description">
        <strong>Añadir Tarea:</strong> Ingresar nuevas tareas manualmente. <br />
        <strong>Lista de Tareas:</strong> Visualizar todas las tareas extraídas desde la API, con opciones para completarlas o eliminarlas. <br />
        <strong>Vista Combinada:</strong> Combina la funcionalidad de añadir tareas manualmente y ver las tareas de la API.
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: "HomeView",
};
</script>

<style scoped>
body {
  background: linear-gradient(135deg, #e0f7fa, #b2ebf2);
  color: #34495e;
  font-family: 'Helvetica Neue', Arial, sans-serif;
}

.container {
  max-width: 900px;
  padding: 30px;
  background-color: rgba(255, 255, 255, 0.95);
  border-radius: 12px;
  box-shadow: 0 8px 30px rgba(0, 0, 0, 0.1);
  transition: transform 0.2s;
}

.container:hover {
  transform: translateY(-5px);
}

.display-4 {
  font-weight: 700;
  color: #20b2aa;
  text-shadow: 1px 1px 5px rgba(0, 0, 0, 0.1);
}

h2 {
  font-weight: 600;
  color: #20b2aa;
  margin-top: 20px;
}

.lead {
  font-size: 1.25rem;
  color: #004d40;
  margin-bottom: 20px;
}

.description {
  font-size: 1rem;
  color: #555;
  line-height: 1.5;
}

.logo {
  border-radius: 50%;
  border: 5px solid #20b2aa;
  box-shadow: 0 0 30px rgba(0, 123, 255, 0.3);
  transition: transform 0.3s, box-shadow 0.3s;
}

.logo:hover {
  transform: scale(1.1);
  box-shadow: 0 0 50px rgba(0, 123, 255, 0.5);
}
</style>

