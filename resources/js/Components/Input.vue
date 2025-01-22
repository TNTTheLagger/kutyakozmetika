<script>
import Idopontok from './Idopontok.vue';

  export default{
    components:{
      Idopontok
    },
    data(){
      return{
        megmutat:false,
        foglalas:{
            nev:"",
            datum:"",
            ido:""
        }
      }
    },
    mounted(){
        let d = new Date();
        let x = d.toISOString();
        document.getElementById("datum").setAttribute("min",x.split("T")[0]);
    },
    methods:{
        idokuld(p){
            this.foglalas.ido=p;
            if (this.foglalas.nev!= "" && this.foglalas.datum!="")
            {
                this.$emit('foglalaskuld',this.foglalas);
                
            }
        }
    }
    
  }
</script>

<template>
    <div class="card">
        <div class="card-body">
            <h2 class="card-title text-center">Kutyakozmetikus Foglalás</h2>
            <p class="card-text">
                <div class="mb-3">
                    <label for="nev" class="form-label">Név</label>
                    <input type="text" class="form-control" id="nev" @input="megmutat=false" v-model="foglalas.nev">
                </div>
                <div class="mb-3">
                    <label for="datum" class="form-label">Dátum</label>
                    <input type="date" class="form-control" id="datum" @input="megmutat=false" v-model="foglalas.datum">
                </div>
                <input type="button" class="btn btn-primary" value="Időpontok megtekintése" @click="megmutat=true">
            </p>
        </div>
        <Idopontok v-if="megmutat" @idokuld="idokuld"/>
    </div>
</template>

<style scoped>

</style>