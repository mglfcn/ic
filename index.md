<div id="selectorLab">
<p>¿En qué laboratorio estás?</p>

<button onclick="setLab('lab1')">Laboratorio 1</button>
<button onclick="setLab('lab2')">Laboratorio 2</button>
<button onclick="setLab('lab3')">Laboratorio 3</button>
</div>

<button onclick="localStorage.removeItem('laboratorio'); location.reload();">
Cambiar laboratorio
</button>
<div class="lab lab1">
<h2>Contenido para laboratorio 1</h2>
</div>

<div class="lab lab2 lab3">
<h2>Contenido para laboratorio 2</h2>
</div>

<div class="lab lab3">
<h2>Contenido para laboratorio 3</h2>
</div>


<script>
function setLab(lab){
  localStorage.setItem("laboratorio", lab);
  mostrarLab();
}

function mostrarLab(){
  const lab = localStorage.getItem("laboratorio");

  if(!lab) return;

  document.querySelectorAll(".lab").forEach(e=>{
    e.style.display="none";
  });

  document.querySelectorAll("."+lab).forEach(e=>{
    e.style.display="block";
  });
}

mostrarLab();
</script>


# Instrucciones

## Si estás en una de las salas de Informática de centro (A1, A2, A3, 1, 3, 4, 5, 6)
1. Abre la carpeta ‘Software_Disponible’ que está en el escritorio y haz doble clic en el enlace directo ‘Safe Exam Browser 3.10’ para ejecutar SEB. 
   Si no consigues encontrarlo [aquí](https://mglfcn.github.io/ic/alternativas.html) tienes otras formas de hacerlo. 
2. Descarga y abre el fichero [config.seb](https://mglfcn.github.io/ic/config.seb)

## Si estás en un laboratorio del DIIS (0.01, 0.02, 0.03, 0.04, 0.05, 0.06, 1.02, 2.11, Sala 2)
1. Descarga y abre el fichero [config.seb](https://mglfcn.github.io/ic/config.seb)
