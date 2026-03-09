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
<p>¿En qué laboratorio estás?</p>

<button class="labbtn" data-lab="lab1">Laboratorio 1</button>
<button class="labbtn" data-lab="lab2">Laboratorio 2</button>
<button class="labbtn" data-lab="lab3">Laboratorio 3</button>

</div>

<div class="lab lab1">
<h2>Contenido para laboratorio 1</h2>
</div>

<div class="lab lab2">
<h2>Contenido para laboratorio 2</h2>
</div>

<div class="lab lab3">
<h2>Contenido para laboratorio 3</h2>
</div>

<!-- <button onclick="localStorage.removeItem('laboratorio'); location.reload();">
Cambiar laboratorio
</button> -->

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

# Instrucciones

## Si estás en una de las salas de Informática de centro (A1, A2, A3, 1, 3, 4, 5, 6)
1. Abre la carpeta ‘Software_Disponible’ que está en el escritorio y haz doble clic en el enlace directo ‘Safe Exam Browser 3.10’ para ejecutar SEB. 
   Si no consigues encontrarlo [aquí](https://mglfcn.github.io/ic/alternativas.html) tienes otras formas de hacerlo. 
2. Descarga y abre el fichero [config.seb](https://mglfcn.github.io/ic/config.seb)

## Si estás en un laboratorio del DIIS (0.01, 0.02, 0.03, 0.04, 0.05, 0.06, 1.02, 2.11, Sala 2)
1. Descarga y abre el fichero [config.seb](https://mglfcn.github.io/ic/config.seb)
