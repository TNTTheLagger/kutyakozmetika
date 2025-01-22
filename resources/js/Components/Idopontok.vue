<script>


  export default{
    components:{
      
    },
    data(){
      return{
        
      }
    }
    
  }
</script>

<template>
    <div class="text-center" v-for="i in 9">
        <input type="button" class="btn btn-success w-50 my-1" :value="i+7+':00'" @click="this.$emit('idokuld',i+7+':00:00')">
    </div>
</template>

<style scoped>

</style>