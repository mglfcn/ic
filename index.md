<style>
.lab {
  display:none;
}

.labbtn {
  padding:6px 12px;
  margin:4px;
}

.labbtn.activo {
  background:#007acc !important;
  color:white !important;
  border:2px solid #005999 !important;
}
</style>

<div id="selectorLab">
<h2>¿En qué laboratorio/sala estás?</h2>

<button class="labbtn" data-lab="lab1">L 0.01</button>
<button class="labbtn" data-lab="lab2">L 0.02</button>
<button class="labbtn" data-lab="lab3">L 0.03</button>
<button class="labbtn" data-lab="salaA1">Sala A1</button>
<button class="labbtn" data-lab="salaA2">Sala A2</button>
<button class="labbtn" data-lab="salaA3">Sala A3</button>
</div>

<script>
function mostrarLab(){

  const lab = localStorage.getItem("laboratorio");

  document.querySelectorAll(".lab").forEach(e=>{
    e.style.display="none";
  });

  document.querySelectorAll(".labbtn").forEach(b=>{
    b.classList.remove("activo");
  });

  if(!lab) return;

  document.querySelectorAll("." + lab).forEach(e=>{
    e.style.display="block";
  });

  const boton = document.querySelector('.labbtn[data-lab="'+lab+'"]');
  if(boton) boton.classList.add("activo");
}

document.querySelectorAll(".labbtn").forEach(b=>{
  b.addEventListener("click",function(){
    const lab=this.dataset.lab;
    localStorage.setItem("laboratorio",lab);
    mostrarLab();
  });
});

mostrarLab();

</script>

<div class="lab salaA1 salaA2 salaA3" markdown="1">
## Instrucciones para las salas de Informática de centro (A1, A2, A3, 1, 3, 4, 5, 6)
1. Abre la carpeta ‘Software_Disponible’ que está en el escritorio y haz doble clic en el enlace directo ‘Safe Exam Browser 3.10’ para ejecutar SEB. 
   Si no consigues encontrarlo [aquí](https://mglfcn.github.io/ic/alternativas.html) tienes otras formas de hacerlo. 
2. Descarga y abre el fichero [config.seb](https://mglfcn.github.io/ic/config.seb)
</div>

<div class="lab lab1 lab2 lab3" markdown="1">
## Intrucciones para los laboratorios del DIIS (0.01, 0.02, 0.03, 0.04, 0.05, 0.06, 1.02, 2.11, Sala 2)
1. Descarga y abre el fichero [config.seb](https://mglfcn.github.io/ic/config.seb)
</div>
