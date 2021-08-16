<script lang="ts">
  let input = "";
  let output = "";
  let binaryMode = false;

  const handleConversion = (e) => {
    // extract the value property
    let {value} = e.target;

    input = value
  }

  // to binary usando manipulação de array
  const toBinary = (n:number) :number => 
    n.toString().split('').reverse().map( (n, i) => n=='1'? 2**i : 0 ).reduce((a,b) => a+b, 0)

  const toDecimal = (x:number) :number => {
    let bin = 0;
    let rem, i = 1;
    while (x != 0) {
        rem = x % 2;
        x = parseInt(x / 2);
        bin = bin + rem * i;
        i = i * 10;
    }
    return bin;
  }

  const updateConversion = (value:string) => {
    // check if isnt a number
    let nvalue = parseInt(value);

    if(isNaN(nvalue)){
      return "Favor, entrada de um binário ou decimal válido"
    }
    else{
      // binary mode?
      if(binaryMode){
        // regexp de binary válido
        // if(!/[^2-9]*[0-1]+/.test(value)) return "Favor, binário inválido"
        return  toDecimal(nvalue).toString()
      }
      else return toBinary(nvalue).toString()
    }
  }

  $: output = updateConversion(input)
</script>

<!-- exercicio 9 -->
<div class="wrapper">
  <label for="">
    Digite número
    {#if binaryMode}
    decimal
    {:else}
    binário
    {/if}
    <input type="text" bind:value={input} on:input={handleConversion}>
  </label>
  <label for="">
    
    <input type="checkbox" bind:checked={binaryMode}>
  </label>
  <span>{output}</span>
</div>
<!-- todo: routerizar os exercicios -->

<style lang="sass">
  .wrapper
    width: 60vw
    height: 60vh
    margin: auto auto
    display: flex
    flex-direction: column
</style>
