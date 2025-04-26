<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Registro de Citas - Clínica Odontológica</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f0f4f8;
      margin: 0;
      padding: 0;
    }
    .container {
      width: 90%;
      max-width: 500px;
      margin: 50px auto;
      padding: 20px;
      background: #ffffff;
      border-radius: 10px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
    }
    h2 {
      text-align: center;
      color: #2c3e50;
    }
    label {
      display: block;
      margin-top: 15px;
      font-weight: bold;
    }
    input, textarea {
      width: 100%;
      padding: 10px;
      margin-top: 5px;
      border-radius: 5px;
      border: 1px solid #ccc;
      box-sizing: border-box;
    }
    button {
      margin-top: 20px;
      width: 100%;
      background-color: #2ecc71;
      color: white;
      border: none;
      padding: 12px;
      font-size: 16px;
      border-radius: 5px;
      cursor: pointer;
    }
    button:hover {
      background-color: #27ae60;
    }
    .message {
      text-align: center;
      margin-top: 15px;
      font-size: 14px;
      color: green;
    }
  </style>
</head>
<body>
  <div class="container">
    <h2>Registro de Citas</h2>
    <form id="citaForm">
      <label for="nombre">Nombre Completo</label>
      <input type="text" id="nombre" required>

      <label for="correo">Correo Electrónico</label>
      <input type="email" id="correo" required>

      <label for="telefono">Teléfono</label>
      <input type="tel" id="telefono" required>

      <label for="fecha">Fecha de la Cita</label>
      <input type="date" id="fecha" required>

      <label for="motivo">Motivo de la Cita</label>
      <textarea id="motivo" rows="4" required></textarea>

      <button type="submit">Registrar Cita</button>
      <div class="message" id="mensajeExito"></div>
    </form>
  </div>

  <!-- Firebase SDK -->
  <script type="module">
    // Importar módulos de Firebase
    import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
    import { getFirestore, collection, addDoc } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";

    // Configuración de Firebase
    const firebaseConfig = {
      apiKey: "AIzaSyDHmfex-G-UTEacg1MvEGhuZ5U7ABQyjNI",
      authDomain: "e1459-68e4a.firebaseapp.com",
      projectId: "e1459-68e4a",
      storageBucket: "e1459-68e4a.appspot.com",
      messagingSenderId: "891435086293",
      appId: "1:891435086293:web:8874ae4de27145f393cd5c"
    };

    // Inicializar Firebase
    const app = initializeApp(firebaseConfig);
    const db = getFirestore(app);

    // Capturar formulario
    const citaForm = document.getElementById("citaForm");
    const mensajeExito = document.getElementById("mensajeExito");

    citaForm.addEventListener("submit", async (e) => {
      e.preventDefault();

      const nombre = document.getElementById("nombre").value;
      const correo = document.getElementById("correo").value;
      const telefono = document.getElementById("telefono").value;
      const fecha = document.getElementById("fecha").value;
      const motivo = document.getElementById("motivo").value;

      try {
        await addDoc(collection(db, "citas"), {
          nombre,
          correo,
          telefono,
          fecha,
          motivo,
          timestamp: new Date()
        });

        mensajeExito.textContent = "¡Cita registrada con éxito!";
        citaForm.reset();
      } catch (error) {
        console.error("Error al registrar la cita: ", error);
        mensajeExito.textContent = "Ocurrió un error. Intenta nuevamente.";
        mensajeExito.style.color = "red";
      }
    });
  </script>
</body>
</html>
