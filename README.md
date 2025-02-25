<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Registro y Denuncias</title>
</head>
<body>

    <h2>Formulario de Registro</h2>
    <form id="registroForm">
        <label>Nombre:</label>
        <input type="text" id="nombre" required><br><br>

        <label>Email:</label>
        <input type="email" id="email" required><br><br>

        <label>Documento de Identidad:</label>
        <input type="text" id="documento" required><br><br>

        <button type="submit">Registrar</button>
    </form>

    <h2>Formulario de Denuncia</h2>
    <form id="denunciaForm">
        <label>Nombre:</label>
        <input type="text" id="denunciaNombre" required><br><br>

        <label>Documento de Identidad:</label>
        <input type="text" id="denunciaDocumento" required><br><br>

        <label>Tipo de Denuncia:</label>
        <select id="tipoDenuncia" required>
            <option value="">Seleccione una opción</option>
            <option value="Robo">Robo</option>
            <option value="Asalto">Asalto</option>
            <option value="Vandalismo">Vandalismo</option>
            <option value="Otro">Otro</option>
        </select><br><br>

        <label>Descripción:</label>
        <textarea id="descripcion" rows="4" required></textarea><br><br>

        <button type="submit">Enviar Denuncia</button>
    </form>

    <!-- Firebase SDK -->
    <script type="module">
        // Importar Firebase
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getDatabase, ref, push, set } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-database.js";

        // Configuración de Firebase
        const firebaseConfig = {
            apiKey: "AIzaSyBICRoE1Xb4JkTta_1hzd_kHc3U1z_Ntms",
            authDomain: "arequipasegura-4b783.firebaseapp.com",
            databaseURL: "https://arequipasegura-4b783-default-rtdb.firebaseio.com",
            projectId: "arequipasegura-4b783",
            storageBucket: "arequipasegura-4b783.firebasestorage.app",
            messagingSenderId: "940832077063",
            appId: "1:940832077063:web:16a3d4723b1e9be93681a2"
        };

        // Inicializar Firebase
        const app = initializeApp(firebaseConfig);
        const database = getDatabase(app);

        // Función para registrar usuarios
        document.getElementById("registroForm").addEventListener("submit", function(event) {
            event.preventDefault(); // Evita recargar la página

            const nombre = document.getElementById("nombre").value;
            const email = document.getElementById("email").value;
            const documento = document.getElementById("documento").value;

            const userRef = ref(database, 'usuarios/');
            const newUserRef = push(userRef);

            set(newUserRef, {
                nombre: nombre,
                email: email,
                documento: documento
            }).then(() => {
                alert("Usuario registrado correctamente");
                document.getElementById("registroForm").reset();
            }).catch((error) => {
                alert("Error al registrar: " + error);
            });
        });

        // Función para enviar denuncias
        document.getElementById("denunciaForm").addEventListener("submit", function(event) {
            event.preventDefault(); // Evita recargar la página

            const nombre = document.getElementById("denunciaNombre").value;
            const documento = document.getElementById("denunciaDocumento").value;
            const tipoDenuncia = document.getElementById("tipoDenuncia").value;
            const descripcion = document.getElementById("descripcion").value;

            const denunciaRef = ref(database, 'denuncias/');
            const newDenunciaRef = push(denunciaRef);

            set(newDenunciaRef, {
                nombre: nombre,
                documento: documento,
                tipoDenuncia: tipoDenuncia,
                descripcion: descripcion,
                fecha: new Date().toISOString()
            }).then(() => {
                alert("Denuncia enviada correctamente");
                document.getElementById("denunciaForm").reset();
            }).catch((error) => {
                alert("Error al enviar la denuncia: " + error);
            });
        });

    </script>

</body>
</html>           
