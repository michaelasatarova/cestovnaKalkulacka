<template>
  <div class="hello" id="poistenie">
      <div class="container bg-light py-5">
        <h1 class="my-3"><strong>Poistenie</strong></h1>
        <div class="base-width">
          
          <form action="">
              <div class="row">           
                <div class="col mt-3">
                 <label> <h5><strong>Variant Poistenia</strong></h5></label>
                </div>

                <div class="col">
                  <select  id="insurance" v-model="selected" required>
                    <option value="" selected></option>
                    <option  name="celorocne" value="dlhodobe" >Celoročné poistenie</option>
                    <option name ="kratkodobe" value="kratkodobe" >Krátkodobe poistenie</option>
                  </select>
                </div>           
              </div>

                <div v-if="selected === 'kratkodobe'" >
                    <div class="row">           
                    <div class="col mt-3">
                    <label> <h5><strong>Začiatok Poistenia</strong></h5></label>
                    </div>

                    <div class="col">             
                    <input type="date"  v-model="dateStart" id="insStart" >
              <!--<datepicker :readonly="true" format="DD.MM.YYYY" name="date1" :value="state" ></datepicker>	-->       					
                    </div>           
                  </div>

                  <div class="row">           
                    <div class="col mt-3">
                      <label><h5><strong>Koniec Poistenia</strong></h5></label>
                    </div>

                    <div class="col">             
                      <input type="date" v-model="dateEnd">						
                    </div>            
                  </div>
              </div>


              <div class="row">           
                <div class="col mt-3">
                  <label><h5><strong>Variant Poistenia</strong></h5></label>
                </div>

                <div class="col">
                  <select  id="insurance2" required>
                    <option value="" selected></option>
                    <option value="zakladny">Základný</option>
                    <option value="rozsireny">Rozšírený</option>
                    <option value="extra">Extra</option>
                  </select>
                </div>           
              </div>

              <div class="row">           
                <div class="col-5 m-3">
                  <label><h5><strong>Storno cesty</strong></h5></label>
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
                  <label><h5><strong>Cena Poistenia</strong></h5></label>
                </div>

                <div class="col">             
                  <input type="text" :placeholder="[[final]]"> 
                  <div class="btn btn-primary mt-3" @click="onChange()" >Vypočítaj</div>
                  
              </div>

            </div> 
       </form>     
      </div>
  </div>
  </div>
</template>

<script>
//import datepicker from 'vue-date-picker';

export default{
        components: {
                  // datepicker,
              },
        data: function(){
          return{
            selected: '',
            dateStart: '',
            dateEnd: '',
            final: '',
           
          }
        },
      
        methods:{
            onChange() {
               let insurance = document.getElementById('insurance'); 
               let insurance2 = document.getElementById('insurance2');
               
          
                //vyparsuje zvolený dátum v milisekundách (den ma 86400000 ms) a vysledok vydelíš dnom, nasledne jedno od druheho odčitaš a to +1 je že zahrna už aj zvolený den
               let date1 = Date.parse(this.dateStart)/86400000;
               let date2 = Date.parse(this.dateEnd)/86400000;
               
  
              //celoročné,zakladne
                if(insurance.value == "dlhodobe" && insurance2.value == "zakladny" ){
                return this.final = 39 +'€';
              }
              //celoročné,rozsireny
              else if(insurance.value == "dlhodobe" && insurance2.value == "rozsireny"){
                return this.final = 49 +'€';
              }
              //celoročné,extra
              else if(insurance.value == "dlhodobe" && insurance2.value == "extra"){
                return this.final = 59 +'€';
              }
              // kratkodobe zakladny
              else if(insurance.value == "kratkodobe" && insurance2.value == "zakladny"){            
                 return this.final = ((date2 - date1 + 1) * 1.2).toFixed(2) + '€'; 
              }
              // kratkodobe rozsireny
              else if(insurance.value == "kratkodobe" && insurance2.value == "rozsireny"){              
                  return this.final = ((date2 - date1 + 1) * 1.8).toFixed(2) + '€'; 
              }
               // kratkodobe extra
              else if(insurance.value == "kratkodobe" && insurance2.value == "extra"){           
                  return this.final = ((date2 - date1 + 1) * 2.4).toFixed(2) + '€'; 
              }            
              else{
                  return this.final =  'Vyplň všetky povinne polia'; 
              }
             },

          getDate(date) {
            console.log("current date", date);
          }, 
          
        },
      }


</script>


<style src="@/assets/sass/app.scss" lang="scss"> 

</style>
