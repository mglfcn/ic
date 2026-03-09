<div id="contenido-especial" style="display: none;">
  Este mensaje solo es para el rango de red permitido.
</div>
# Instrucciones
<!-- ## Si estás en una de las salas de Informática de centro (A1, A2, A3, 1, 3, 4, 5, 6)
1. Abre la carpeta ‘Software_Disponible’ que está en el escritorio y ejecuta SEB haciendo doble clic en el enlace directo ‘Safe Exam Browser 3.10’.  
   Si la carpeta no existe o no está el acceso directo haz doble clic en el icono 'Recargar la carpeta Software_Disponible' (disponible en el escritorio) y creará de nuevo la carpeta.
   Si no consigues encontrarlo [aquí](https://mglfcn.github.io/ic/alternativas.html) tienes otras formas de ejecutar SEB.
3. Descarga y abre el fichero [config.seb](https://mglfcn.github.io/ic/config.seb) -->

## Si estás en un laboratorio del DIIS (0.01, 0.02, 0.03, 0.04, 0.05, 0.06, 1.02, 2.11, Sala 2)
1. Descarga y abre el fichero [config.seb](https://mglfcn.github.io/ic/config.seb)

<script>
function ipToInt(ip){
  return ip.split('.').reduce((acc,oct)=> (acc<<8) + parseInt(oct),0) >>> 0;
}

function ipInRange(ip, start, end){
  const n = ipToInt(ip);
  return n >= ipToInt(start) && n <= ipToInt(end);
}

fetch("https://api.ipify.org?format=json")
  .then(r => r.json())
  .then(data => {
    const ip = data.ip;

    if (ipInRange(ip,"155.210.152.50","155.210.152.55")) {
      document.getElementById("contenido-especial").style.display = "block";
    }
  });
</script>
