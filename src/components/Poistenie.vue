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
              <select  id="insurance">
                <option  name="celorocne" value="dlhodobe" >Celoročné poistenie</option>
							  <option name ="kratkodobe" value="kratkodobe" >Krátkodobé poistenie</option>
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
              <select  id="insurance2">
                <option value="zakladny">Základný</option>
                <option value="rozsireny">Rozšírený</option>
                <option value="extra">Extra</option>
              </select>
            </div>           
          </div>

           <div class="row">           
            <div class="col-5 m-3">
              <h5><strong>Storno cesty</strong></h5>
            </div>

          <div class="col">
            <div class="row">
              <div class="col m-3 form-check">
                  <input class="form-check-input" type="radio" name="storno" id="exampleRadios1" value="option1" >
                  <label class="form-check-label" for="exampleRadios1">
                    ANO
                  </label>          
              </div>
              <div class="col m-3 form-check">
                  <input class="form-check-input" type="radio" name="storno" id="exampleRadios1" value="option1" >
                  <label class="form-check-label" for="exampleRadios1">
                    NIE
                  </label>          
              </div>
            </div>
        </div>
      </div>

      <div class="row">           
            <div class="col-5 m-3">
              <h5><strong>Športove aktivity</strong></h5>
            </div>

          <div class="col">
            <div class="row">
              <div class="col m-3 form-check">
                  <input class="form-check-input" type="radio" name="šport" id="exampleRadios3" value="option3" >
                  <label class="form-check-label" for="exampleRadios3">
                    ANO
                  </label>          
              </div>
              <div class="col m-3 form-check">
                  <input class="form-check-input" type="radio" name="šport" id="exampleRadios4" value="option4" >
                  <label class="form-check-label" for="exampleRadios4">
                    NIE
                  </label>          
              </div>
            </div>
        </div>
      </div>

          <div class="row">           
            <div class="col mt-3">
              <h5><strong>Cena Poistenia</strong></h5>
            </div>

            <div class="col">             
							<input type="text" :placeholder="[['vysledok fungule v konzole']]"> 
              <div class="btn btn-primary mt-3" @click="onChange()" >Vypočítaj</div>
              
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
            onChange() {
               var insurance = document.getElementById('insurance'); 
               var insurance2 = document.getElementById('insurance2');
               
                //vyparsuje zvolený dátum v milisekundách (den ma 86400000 ms) a vysledok vydelíš dnom, nasledne jedno od druheho odčitaš a to +1 je že zahrna už aj zvolený den
               var date1 = Date.parse(this.dateStart)/86400000;
               var date2 = Date.parse(this.dateEnd)/86400000;

              //celoročné,zakladne
                if(insurance.value == "dlhodobe" && insurance2.value == "zakladny" ){
                console.log(39 +'€');
              }
              //celoročné,rozsireny
              else if(insurance.value == "dlhodobe" && insurance2.value == "rozsireny"){
                console.log(49 +'€');
              }
              //celoročné,extra
              else if(insurance.value == "dlhodobe" && insurance2.value == "extra"){
                console.log(59 +'€');
              }
              // kratkodobe zakladny
              else if(insurance.value == "kratkodobe" && insurance2.value == "zakladny"){            
                 console.log(((date2 - date1 + 1) * 1.2).toFixed(2) + '€'); 
              }
              // kratkodobe rozsireny
              else if(insurance.value == "kratkodobe" && insurance2.value == "rozsireny"){              
                  console.log(((date2 - date1 + 1) * 1.8).toFixed(2) + '€'); 
              }
               // kratkodobe extra
              else if(insurance.value == "kratkodobe" && insurance2.value == "extra"){           
                  console.log(((date2 - date1 + 1) * 2.4).toFixed(2) + '€'); 
              }            
              else{
                  console.log('Vyplň všetky povinne polia'); 
              }
             },
        },
      }


</script>


<style src="@/assets/sass/app.scss" lang="scss"> 

</style>
