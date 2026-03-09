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
function getLocalIPs(callback) {
  const pc = new RTCPeerConnection({iceServers: []});
  pc.createDataChannel("");

  pc.onicecandidate = function(event) {
    if (!event || !event.candidate) return;

    const candidate = event.candidate.candidate;
    const match = candidate.match(/([0-9]{1,3}(\.[0-9]{1,3}){3})/);

    if (match) {
      callback(match[1]);
    }
  };

  pc.createOffer()
    .then(offer => pc.setLocalDescription(offer))
    .catch(console.error);
}

getLocalIPs(function(ip){
  console.log("IP local:", ip);

  if (ip.startsWith("10.3.16.")) {
    document.getElementById("contenido-lab").style.display="block";
  }
});
</script>
