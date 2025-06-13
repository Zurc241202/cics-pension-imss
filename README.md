# cics-pension-imss
simulador de pension tipo SINDO/CICS IMSS
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>CONSULTA DE PENSIÓN - IMSS CICS</title>
  <style>
    body {
      background-color: black;
      color: white;
      font-family: Courier, monospace;
      font-size: 13px;
      text-transform: uppercase;
      padding: 20px;
    }
    input, button {
      background: #111;
      color: white;
      border: 1px solid turquoise;
      padding: 6px;
      font-family: Courier;
    }
    .resultado {
      margin-top: 20px;
      border: 1px dashed turquoise;
      padding: 15px;
      white-space: pre-line;
    }
    .reloj {
      float: right;
      color: #bbb;
      font-size: 11px;
    }
  </style>
</head>
<body>
  <div class="reloj" id="reloj"></div>
  <h2>MODULO CICS-SINDO IMSS</h2>
  <p>INGRESE SU NÚMERO DE SEGURO SOCIAL PARA CONSULTAR SU PENSIÓN:</p>
  <input type="text" id="nss" placeholder="EJEMPLO: 92916600478">
  <button onclick="consultar()">CONSULTAR</button>
  <button onclick="window.print()">IMPRIMIR</button>

  <div class="resultado" id="resultado"></div>

  <script>
    function actualizarHora() {
      const ahora = new Date();
      const opciones = { timeZone: 'America/Mexico_City', hour12: false };
      const hora = ahora.toLocaleTimeString('es-MX', opciones);
      const fecha = ahora.toLocaleDateString('es-MX', opciones);
      document.getElementById("reloj").innerText = "CDMX: " + fecha + " " + hora;
    }
    setInterval(actualizarHora, 1000);
    actualizarHora();

    function consultar() {
      const nss = document.getElementById("nss").value.trim();
      const salida = document.getElementById("resultado");
      const datos = {
        "92916600478": {
          nombre: "LUCIO NICEFORO CRUZ",
          nacimiento: "09/02/1963",
          regimen: "CESANTIA",
          semanas: 2500,
          mensual: "$50,540.80",
          retro: "4 MESES",
          primerpago: "01/07/2025"
        },
        "92907232687": {
          nombre: "EUGENIA BENÍTEZ JIMÉNEZ",
          nacimiento: "15/10/1965",
          regimen: "CESANTIA",
          semanas: 2340,
          mensual: "$43,280.40",
          retro: "3 MESES",
          primerpago: "01/07/2025"
        }
      };

      if (datos[nss]) {
        const d = datos[nss];
        salida.innerText =
          `NOMBRE DEL ASEGURADO: ${d.nombre}
NSS: ${nss}
FECHA DE NACIMIENTO: ${d.nacimiento}
RÉGIMEN: ${d.regimen}
SEMANAS COTIZADAS: ${d.semanas}
PENSIÓN MENSUAL: ${d.mensual}
RETROACTIVO: ${d.retro}
PRIMER PAGO PROGRAMADO: ${d.primerpago}`;
      } else {
        salida.innerText = "SERVICIO NO DISPONIBLE O NSS NO RECONOCIDO.";
      }
    }
  </script>
</body>
</html>
