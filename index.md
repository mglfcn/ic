# Instrucciones

<div id="contenido-sala" style="display: none;" markdown="1">
## Según tu IP estás en una de las salas de Informática de centro (A1, A2, A3, 1, 3, 4, 5, 6)
1. Abre la carpeta ‘Software_Disponible’ que está en el escritorio y haz doble clic en el enlace directo ‘Safe Exam Browser 3.10’ para ejecutar SEB. 
   Si no consigues encontrarlo [aquí](https://mglfcn.github.io/ic/alternativas.html) tienes otras formas de hacerlo. 
2. Descarga y abre el fichero [config.seb](https://mglfcn.github.io/ic/config.seb)
</div>

<div id="contenido-lab" style="display: none;" markdown="1">
## Según tu IP estás en un laboratorio del DIIS (0.01, 0.02, 0.03, 0.04, 0.05, 0.06, 1.02, 2.11, Sala 2)
1. Descarga y abre el fichero [config.seb](https://mglfcn.github.io/ic/config.seb)
</div>

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

    if (ipInRange(ip,"10.3.16.41","10.3.16.155")||
        ipInRange(ip,"10.3.17.3","10.3.17.183")||
        ipInRange(ip,"155.210.154.191","155.210.154.210")) {
      document.getElementById("contenido-lab").style.display = "block";
    }else{
     document.getElementById("contenido-sala").style.display = "block";
    }
  });
</script>
