<style>
  .card {
    height: fit-content;
    background: rgba(255, 255, 255, 0.2);
    border: solid 1px rgba(255, 255, 255, 0.7);
    border-radius: 5px;
    padding: 2rem 2rem 1rem 2rem;
    box-shadow: 0px 8px 20px rgba(0, 0, 0, 0.15);
    flex-direction: column;
    backdrop-filter: blur(20px);
    z-index: 100;
    transition: width 1s, height 350ms;
  }

  
      .circle {
        width: 300px;
        height: 300px;
        border-radius: 50%;
        filter: blur(60px);
      }

      .circlebg {
        display: flex;
        position: absolute;
        z-index: -2;
        opacity: 0.7;
      }
      .circle-red {
        background: red;
        transform: translateX(40%);
      }

      .circle-blue {
        background-color: blue;
        transform: translateX(-40%);
      }

      .circle-green {
        background-color: green;
      }

      .circle-yellow {
        background-color: yellow;
        transform: translateX(-80%);
      }

</style>
<script>
  export let title = '';
  export let img='';
  let imgDisplay = 'none'
  $: {
    if (img != '') {
      imgDisplay = 'block'
    }
  }
</script>

<div class="circlebg">
  <!-- <div class="circle circle-red"></div> -->
  <!-- <div class="circle circle-green"></div>
  <div class="circle circle-blue"></div> -->
  <!-- <div class="circle circle-yellow"></div> -->
</div>
<div class="card">
  <div class="">
    <h5>{title}</h5>
  </div>
  <div>
    <img src={img}  alt="img" style={`display:${imgDisplay}`} width="100%">
  </div>
</div>