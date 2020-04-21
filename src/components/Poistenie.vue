<template>
  <div class="hello" id="app">
      <div class="container bg-light py-5">
        <h1 class="my-3"><strong>Poistenie</strong></h1>
        <div class="base-width">
          
          <div class="row">           
            <div class="col mt-3">
              <h5><strong>Variant Poistenia</strong></h5>
            </div>

            <div class="col">
              <select name="" id="" @change="onChange($event)"  >
                <option  name= "celorocne" value="39" id="dlhodobe">Celoročné poistenie</option>
							<option name ="kratkodobe" value="1,2 * počet dní " id="kratkodobe">Krátkodobé poistenie</option>
              </select>
            </div>           
          </div>

            <div class="row">           
            <div class="col mt-3">
              <h5><strong>Začiatok Poistenia</strong></h5>
            </div>

            <div class="col">             
							<input type="date">						
            </div>           
          </div>

          <div class="row">           
            <div class="col mt-3">
              <h5><strong>Koniec Poistenia</strong></h5>
            </div>

            <div class="col">             
							<input type="date">						
            </div>            
          </div>

          <div class="row">           
            <div class="col mt-3">
              <h5><strong>Variant Poistenia</strong></h5>
            </div>

            <div class="col">
              <select name="" id="">
                <option value="">Základný</option>
                <option value="">Rozšírený</option>
                <option value="">Extra</option>
              </select>
            </div>           
          </div>

          <div class="row">           
            <div class="col mt-3">
              <h5><strong>Cena Poistenia</strong></h5>
            </div>

            <div class="col">             
							<input type="text"> 
              
          </div>

        </div>       
      </div>
  </div>
  </div>
</template>

<script>

export default{
        data: function(){
          return{
            status: 'Critical',
           
          }
        },
        methods:{
          kratkodobe(){
           return document.getElementById('kratkodobe').value + '€';
             
          },         
          dlhodobe(){
            return document.getElementById('dlhodobe').value + '€';
          },
          onChange(event){
            console.log(event.target.value) ;
        }
        },
      }


</script>


<style src="@/assets/sass/app.scss" lang="scss"> 

</style>
