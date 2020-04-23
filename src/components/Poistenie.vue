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
              <select  id="insurance" @change="onChange($event)">
                <option  name= "celorocne" :value="dlhodobe()" >Celoročné poistenie</option>
							  <option name ="kratkodobe" :value="kratkodobe()" >Krátkodobé poistenie</option>
              </select>
            </div>           
          </div>

            <div class="row">           
            <div class="col mt-3">
              <h5><strong>Začiatok Poistenia</strong></h5>
            </div>

            <div class="col">             
							<input type="date" v-model="dateStart" >						
            </div>           
          </div>

          <div class="row">           
            <div class="col mt-3">
              <h5><strong>Koniec Poistenia</strong></h5>
            </div>

            <div class="col">             
							<input type="date" v-model="dateEnd">						
            </div>            
          </div>

          <div class="row">           
            <div class="col mt-3">
              <h5><strong>Variant Poistenia</strong></h5>
            </div>

            <div class="col">
              <select name="" id="">
                <option value="#">Základný</option>
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
							<input type="text" :placeholder="[[ kratkodobe()]]"> 
             
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
            dateStart: '',
            dateEnd: '',
          }
        },
        methods:{
            onChange(event) {
              console.log(event.target.value);
             },
            kratkodobe(){
                 //vyparsuje zvolený dátum v milisekundách (den ma 86400000 ms) a vysledok vydelíš dnom, nasledne jedno od druheho odčitaš a to +1 je že zahrna už aj zvolený den
            // to 1,2 je kratkodobe poistenie zakladný balík ale bude sa ešte meniť
                var date1 = Date.parse(this.dateStart)/86400000;
                var date2 = Date.parse(this.dateEnd)/86400000;
                  console.log(((date2 - date1 + 1) * 1.2).toFixed(2) + '€'); 
            },
            dlhodobe(){
                console.log(39 +'€'); 
            },

        },
      }


</script>


<style src="@/assets/sass/app.scss" lang="scss"> 

</style>
