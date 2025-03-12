<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Plantilla de Caso de Uso</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #d5d4e3;
        }
        .container {
            max-width: 700px;
            margin: 50px auto;
            padding: 50px;
            background: #a5a1c8;
            border-radius: 10px;
            box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
        }
        h2 {
            text-align: center;
            color: #333;
        }
        label {
            font-weight: bold;
            color: #333;
            display: block;
            margin-top: 10px;
        }
        input, textarea {
            width: 100%;
            padding: 8px;
            margin-top: 5px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        textarea {
            height: 80px;
        }
        button {
            background-color: #007bff;
            color: white;
            padding: 12px;
            border: none;
            width: 100%;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
            margin-top: 15px;
        }
        button:hover {
            background-color: #0056b3;
        }
    </style>
</head>
<body>
    <div class="container">
        <h2>Plantilla de Caso de Uso</h2>
        <label>Nombre del Caso de Uso:</label>
        <input type="text" id="nombre" placeholder="Ejemplo: Realizar Pago con Tarjeta">
        <label>Descripción:</label>
        <textarea id="descripcion" placeholder="Breve descripción del caso de uso"></textarea>
        <label>Actor(es):</label>
        <input type="text" id="actores" placeholder="Ejemplo: Cliente, Sistema de Pago">
        <label>Precondiciones:</label>
        <textarea id="precondiciones" placeholder="Condiciones previas necesarias"></textarea>
        <label>Flujo Normal:</label>
        <textarea id="flujo" placeholder="Pasos secuenciales del proceso"></textarea>
        <label>Excepciones:</label>
        <textarea id="excepciones" placeholder="Posibles errores y cómo manejarlos"></textarea>
        <label>Postcondiciones:</label>
        <textarea id="postcondiciones" placeholder="Estado final después de la ejecución"></textarea>
        <button onclick="generarPDF()">Descargar PDF</button>
    </div>
    
    <script>
        function generarPDF() {
            const { jsPDF } = window.jspdf;
            const doc = new jsPDF();
            doc.setFontSize(12);
            
            let y = 30; // Aumenta la distancia después del título
            const margenX = 10;
            const anchoTexto = 180;
            
            doc.setFont(undefined, 'bold');
            doc.setFontSize(16);
            doc.text("Plantilla de Caso de Uso", 105, 20, { align: "center" });
            doc.setFontSize(12);
            
            function agregarCampo(titulo, valor) {
                doc.setFont(undefined, 'bold');
                doc.text(titulo, margenX, y);
                doc.setFont(undefined, 'normal');

                let textoFormateado = doc.splitTextToSize(valor, anchoTexto - 4);
                let altoTexto = textoFormateado.length * 6;
                
                doc.rect(margenX, y + 2, anchoTexto, altoTexto + 4);
                doc.text(textoFormateado, margenX + 2, y + 8);
                
                y += altoTexto + 12;
            }

            agregarCampo("Nombre del Caso de Uso:", document.getElementById("nombre").value);
            agregarCampo("Descripción:", document.getElementById("descripcion").value);
            agregarCampo("Actor(es):", document.getElementById("actores").value);
            agregarCampo("Precondiciones:", document.getElementById("precondiciones").value);
            agregarCampo("Flujo Normal:", document.getElementById("flujo").value);
            agregarCampo("Excepciones:", document.getElementById("excepciones").value);
            agregarCampo("Postcondiciones:", document.getElementById("postcondiciones").value);
            
            doc.save("caso_de_uso.pdf");
        }
    </script>
</body>
</html>
