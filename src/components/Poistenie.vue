<template>
  <div class="hello" id="poistenie">
      <div class="container bg-light py-5">
        <h1 class="my-3"><strong>Poistenie</strong></h1>
        <div class="base-width">
          
          <form @submit.prevent="calculateInsuranceCosts()">
              <div class="row">           
                <div class="col mt-3">
                 <label> <h5><strong>Variant Poistenia</strong></h5></label>
                </div>

                <div class="col">
                  <select  v-model="insurance1"  required>
                    <option value="" selected></option>
                    <option  name="celorocne" value="dlhodobe" >Celoročné poistenie</option>
                    <option name ="kratkodobe" value="kratkodobe" >Krátkodobe poistenie</option>
                  </select>
                </div>           
              </div>

                <div v-if="insurance1 === 'kratkodobe'" required>
                    <div class="row">           
                    <div class="col mt-3">
                    <label> <h5><strong>Začiatok Poistenia</strong></h5></label>
                    </div>

                    <div class="col">             
                    <datepicker
                        v-model="dateStart"
                        :format="DatePickerFormat"
                        :disabledDates="disabledDates">
                    </datepicker>	      					
                    </div>           
                  </div>

                  <div class="row">           
                    <div class="col mt-3">
                      <label><h5><strong>Koniec Poistenia</strong></h5></label>
                    </div>

                    <div class="col">                             
                      <datepicker
                        v-model="dateEnd"
                        :format="DatePickerFormat"
                        :disabledDates="disabledDates">
                    </datepicker>						
                    </div>            
                  </div>
              </div>


              <div class="row">           
                <div class="col mt-3">
                  <label><h5><strong>Balíček Poistenia</strong></h5></label>
                </div>

                <div class="col">
                  <select   v-model="insurance2" required>
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

              <div class="col m-3 text-right">
                <label > Chcem zahrnuť storno
              <input type="checkbox" id="checkboxStorno"  v-model="storno">
              <span class="checkmark"></span>
              </label>
            </div>

          </div>

          <div class="row">           
                <div class="col-5 m-3">
                  <h5><strong>Športove aktivity</strong></h5>
                </div>

              <div class="col m-3 text-right">
                <label > Chcem zahrnuť šport
               <input type="checkbox" id="checkboxSport"  v-model="sport">
               <span class="checkmark"></span>
               </label>
            </div>
            </div>

              <div class="row">           
                <div class="col mt-3">
                  <label><h5><strong>Cena Poistenia</strong></h5></label>
                </div>

                <div class="col">             
                  <input type="text" :placeholder="final">               
                  <button type="submit" class="btn btn-primary mt-3"  >Vypočítaj</button>                                
              </div>

            </div> 
       </form>     
      </div>
  </div>
  </div>
</template>

<script>
import Datepicker from 'vuejs-datepicker';

export default{
        components: {
                   Datepicker,
              },
        data: function(){
          return{
            insurance1: '',
            insurance2: '',        
            final: '', 
            sport: false,
            storno: false,
            selected:'',       
            dateStart:'', 
            dateEnd: '',                        
            DatePickerFormat: 'dd/MM/yyyy',
            disabledDates: {
            to: new Date(Date.now() - 8640000)
                },
             moznosti: {
                dlhodobe: {
                  zakladny: 39,
                  rozsireny: 49,
                  extra: 59,
                },
                kratkodobe:{
                  zakladny: 1.2,
                  rozsireny: 1.8,
                  extra: 2.4,
                }
              },

              }
           },
         

        methods:{
            calculateInsuranceCosts() {            
              const packageValue = this.moznosti[this.insurance1][this.insurance2];

             if(this.insurance1 === 'dlhodobe'){
                  if(this.storno && this.sport){
                    return this.final = (packageValue *  1.2 * 1.1).toFixed(2) + '€'                 
                  }else if(this.sport){
                    return this.final = (packageValue * 1.1).toFixed(2) + '€';
                  }else if(this.storno ){     
                     return this.final = (packageValue * 1.2).toFixed(2) + '€';
                  }else{
                    return this.final =packageValue + '€';
                  }

               }else if(this.insurance1 === 'kratkodobe'){              
               // console.log(this.dateStart.getTime());
                //vyparsuje zvolený dátum v milisekundách (den ma 86400000 ms) a vysledok vydelíš dnom, nasledne jedno od druheho odčitaš a to +1 je že zahrna už aj zvolený den
              let d1 = this.dateStart.getTime();
              let date1= d1 /86400000;
              let d2 = this.dateEnd.getTime();
              let date2 = d2 /86400000;

              let packageWithDate = packageValue*(date2-date1);
             
              
                if(this.storno && this.sport){
                    return this.final = (packageWithDate *  1.5 * 1.3).toFixed(2) + '€'                 
                  }else if(this.sport){
                    return this.final = (packageWithDate * 1.3).toFixed(2) + '€';
                  }else if(this.storno ){     
                     return this.final = (packageWithDate * 1.5).toFixed(2) + '€';
                  }else{
                    return this.final = packageWithDate.toFixed(2) + '€';
                  }
             }
             }
             }
      };
</script>

<style >
/* Hide the browser's default checkbox */
.container input[type='checkbox'] {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}
/* Create a custom checkbox */
.checkmark {
  position: absolute;
  top: 0;
  left: 36px;
  height: 25px;
  width: 25px;
  background-color: #eee;
}

/* On mouse-over, add a grey background color */
.container:hover input ~ .checkmark {
  background-color: #ccc;
}

/* When the checkbox is checked, add a blue background */
.container input:checked ~ .checkmark {
  background-color: #2196F3;
}

/* Create the checkmark/indicator (hidden when not checked) */
.checkmark:after {
  content: "";
  position: absolute;
  display: none;
}

/* Show the checkmark when checked */
.container input:checked ~ .checkmark:after {
  display: block;
}

/* Style the checkmark/indicator */
.container .checkmark:after {
  left: 9px;
  top: 5px;
  width: 5px;
  height: 10px;
  border: solid white;
  border-width: 0 3px 3px 0;
  -webkit-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  transform: rotate(45deg);
}
</style>
