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
<button class="labbtn" data-lab="lab4">L 0.04</button>
<button class="labbtn" data-lab="lab5">L 0.05</button>
<button class="labbtn" data-lab="lab6">L 0.06</button>
<button class="labbtn" data-lab="lab102">L 1.02</button>
<button class="labbtn" data-lab="lab211">L 2.11</button>
<button class="labbtn" data-lab="sala2">Sala 2</button>
<br>
<button class="labbtn" data-lab="salaA1">Sala A1</button>
<button class="labbtn" data-lab="salaA2">Sala A2</button>
<button class="labbtn" data-lab="salaA3">Sala A3</button>
<button class="labbtn" data-lab="sala1">Sala 1</button>
<button class="labbtn" data-lab="sala3">Sala 3</button>
<button class="labbtn" data-lab="sala4">Sala 4</button>
<button class="labbtn" data-lab="sala5">Sala 5</button>
<button class="labbtn" data-lab="sala6">Sala 6</button>
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

<div class="lab salaA1 salaA2 salaA3 sala1 sala3 sala4 sala5 sala6" markdown="1">
## Instrucciones para las salas de Informática de centro (A1, A2, A3, 1, 3, 4, 5, 6)
1. Abre la carpeta ‘Software_Disponible’ que está en el escritorio y haz doble clic en el enlace directo ‘Safe Exam Browser 3.10’ para ejecutar SEB. 
   Si no consigues encontrarlo [aquí](https://mglfcn.github.io/ic/alternativas.html) tienes otras formas de hacerlo. 
2. Descarga y abre el fichero [config.seb](https://mglfcn.github.io/ic/config.seb)
</div>

<div class="lab lab1 lab2 lab3 lab4 lab5 lab6 lab102 lab211 sala2" markdown="1">
## Intrucciones para los laboratorios del DIIS (0.01, 0.02, 0.03, 0.04, 0.05, 0.06, 1.02, 2.11, Sala 2)
1. Descarga y abre el fichero [config.seb](https://mglfcn.github.io/ic/config.seb)
</div>
