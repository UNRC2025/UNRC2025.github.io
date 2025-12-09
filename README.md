<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Solicitud de Expedientes UNRC</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      background-color: #f5f5f5;
    }
    .container {
      background: white;
      padding: 30px;
      border-radius: 8px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
      text-align: center;
      width: 90%;
      max-width: 400px;
    }
    h2 {
      margin-bottom: 20px;
      color: navy;
    }
    label {
      display: block;
      margin-top: 10px;
      text-align: left;
    }
    input, button, textarea {
      width: 100%;
      padding: 10px;
      margin-top: 5px;
      border: 1px solid #ccc;
      border-radius: 4px;
      box-sizing: border-box;
    }
    button {
      margin-top: 15px;
    }
    .btn {
      background-color: navy;
      color: white;
      border: none;
      cursor: pointer;
    }
    .btn:hover {
      background-color: #003366;
    }
    #resultado {
      margin-top: 15px;
      font-weight: bold;
      color: green;
    }
    #form-solicitud {
      margin-top: 20px;
      display: none; /* oculto inicialmente */
    }
    #confirmacion {
      margin-top: 20px;
      font-weight: bold;
      color: darkgreen;
      display: none; /* oculto inicialmente */
    }
    @media (max-width: 480px) {
      .container {
        padding: 20px;
      }
      h2 {
        font-size: 18px;
      }
    }
  </style>
</head>
<body>
  <div class="container">
    <h2>VERIFICACIÓN DE EXPEDIENTES UNRC</h2>
    <form id="form-busqueda">
      <label for="nombre">Nombre completo:</label>
      <input id="nombre" name="nombre" type="text" required>
      <button type="submit">Buscar</button>
    </form>

    <div id="resultado"></div>

    <button id="btn-solicitud" class="btn" style="display:none;">Generar solicitud</button>

    <!-- Formulario de solicitud -->
    <form id="form-solicitud">
      <h2>Solicitud</h2>
      <label for="solicitante">Nombre del solicitante:</label>
      <input id="solicitante" name="solicitante" type="text" required>

      <label for="fecha">Fecha:</label>
      <input id="fecha" name="fecha" type="date" required>

      <label for="detalle">Detalle:</label>
      <textarea id="detalle" name="detalle" rows="4"></textarea>

      <button type="submit" class="btn">Enviar solicitud</button>
    </form>

    <!-- Mensaje de confirmación -->
    <div id="confirmacion">✅ Solicitud enviada correctamente</div>
  </div>

  <script>
    const formBusqueda = document.getElementById('form-busqueda');
    const formSolicitud = document.getElementById('form-solicitud');
    const btnSolicitud = document.getElementById('btn-solicitud');
    const resultado = document.getElementById('resultado');
    const confirmacion = document.getElementById('confirmacion');

    formBusqueda.addEventListener('submit', function(e){
      e.preventDefault();
      const nombre = document.getElementById('nombre').value;
      // Aquí iría la llamada al backend (fetch a tu API)
      resultado.innerText = "Expediente encontrado en archivo";
      btnSolicitud.style.display = "inline-block";
    });

    btnSolicitud.addEventListener('click', function(){
      formSolicitud.style.display = "block";
    });

    formSolicitud.addEventListener('submit', function(e){
      e.preventDefault();
      // Ocultar formulario y mostrar confirmación
      formSolicitud.style.display = "none";
      btnSolicitud.style.display = "none";
      resultado.innerText = "";
      confirmacion.style.display = "block";

      // Reiniciar formularios
      formBusqueda.reset();
      formSolicitud.reset();

      // Ocultar confirmación después de unos segundos y volver al estado inicial
      setTimeout(() => {
        confirmacion.style.display = "none";
      }, 3000);
    });
  </script>
</body>
</html>
