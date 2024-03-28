<!-- Script JS -->
<script>
    import * as d3 from "d3"

  let numbers = [5, 18, 29, 75, 100]
  let numbersDivided5 = numbers.map(n => Math.floor(n / 5))
  let jugadores = ['Baez', 'Cerundolo', 'Thiem', 'Rune', 'Djokovic']
  let barrios = ['Belgrano', 'Nuñez', 'Palermo', 'Recoleta', 'Flores']
  function altura(n) {
    let scale = d3
      .scaleLinear()
      .domain(d3.extent(numbers)) // extent returns [min, max]
      .range([15, 225])
    return scale(n)
  }

  import { fade, fly} from 'svelte/transition';
  let visible = true;
  function alturaColCoffe(n) {
    let scale = d3
      .scaleLinear()
      .domain([0, d3.max(numbers)]) // extent returns [min, max]
      .range([0, 175])
    return scale(n)
  }

</script>

<!-- Estructura contenido HTML -->
<div class="caja">
  <img src="https://www.lanacion.com.ar/resizer/g0F5yQgCBF-JqvwaSaBJr4l24dE=/420x0/filters:format(webp):quality(70)/cloudfront-us-east-1.images.arcpublishing.com/lanacionar/E5FFGHBJ3FGCJAKMRPDEDL4ZSM.png" class="img" alt="">
    <div>
        <h1>Más Victoriosos</h1>
        <h3>Partidos ganados en lo que va del circuito</h3>
        <p>(Solo contando torneos ATP)</p>
    </div>
    <img src="https://ausopen.com/sites/default/files/styles/420x/public/Thiem.png?itok=gtaee8MU" class="imga" alt="">
</div>


<main>

  <!-- Canal: longitud. Type: Isotype Chart  -->

    <label class = "boton" >
        <input type="checkbox" bind:checked={visible} />
        Ver graficos
    </label>
    
    <div class="iso__container-iso">
        
        {#each numbersDivided5 as n, index}
        {#if visible }
        <div class="row" in:fly={{ y: 200, duration: 2000 }} out:fade>
            {#each Array(n) as m}
            <img
                style="height: 50px; padding: 2px"
                src="./images/10p.png"
                alt="tenis ball"
            />
            {/each}
            <p>{numbers[index]} - {jugadores[index]}</p>
        </div>
        {/if}
        {/each}
        
    </div>
    
    <div class="caja">
      <img src="./images/messi.png" class="img2">
      <div>
          <h1>Cantidad de Vino Tomado per capita por Barrio en CABA</h1>
          <h3>Medido en litros</h3>
      </div>
      <img src="./images/vinito.png" class="img2">
  
  </div>
  

    <div class="coffes-container">
        {#each numbers as n, index}
        <div>
          <div class="column-wrapper">
            <div class="column-coffe" style="height: {alturaColCoffe(n)}%;"></div>
            <img class="coffe" src="./images/vinoempt.svg" alt="">
          </div>
          <p class="number">{barrios[index]} - {n}</p>
        </div>
        {/each}
      </div>
    <hr />

</main>


<!-- Estilos CSS -->
<style>
    .img{
      width: 150px;
      height: 200px;
    }
    .img2{
      width: 250px;
      height: 150px;
    }
    .imga{
      width: 200px;
      height: 200px;
    }

    h1 {
        font-family: Helvetica;
        font-weight: bold;
    }
    h3 {
        font-family: Helvetica;
    }
    div.caja {
      display: flex;
        margin-bottom: 0%;
        margin-top: 5%;
        margin-right: auto;
        margin-left: auto;
        width: 80%;
        text-align: center;
        align-items: center;
        justify-content: space-evenly;
    }
    .iso__container-iso {
        display: flex;
        flex-direction: column;
        max-width: 1000px;
        align-items: start;
        justify-content: space-around;
        margin-left: 2%;
    }
    .headline {
        margin-left: 1%;
        text-align: left;
        margin-top: 50px;
        /* border: 1px solid red; */
    }
    label.boton{
        margin-left: 2%;
        font-family: Helvetica;
        font-weight: bold;
        margin-top: 2%;
        margin-bottom: 2%;
    }
    .coffes-container {
    align-items: center;
    margin-top: 500px;
    display: flex;
    justify-content: space-evenly;
  }
  .column-wrapper {
    position: relative;
    width: 160px;
    height: 200px;
    padding-right: 10px;
    /* background-color: #ccc;
    border: black 1px solid; */
  }
   .column-coffe {
    position: absolute;
    height: 50%;
    padding-right: 10px;
    left: 0%;
    right: 10%;
    bottom: 0;
    /* width: 100%;  */
    background-color: rgb(51, 0, 88);
  }
   .coffe {
    padding-right: 10px;
    position: absolute;
    bottom: -10px;
    width: 100%;
  }
   .number {
    text-align: center;
    margin-top: 20px;
    font-weight: 1000;
  }

</style>