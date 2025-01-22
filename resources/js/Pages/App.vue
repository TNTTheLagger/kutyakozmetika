<script>
import Input from '../Components/Input.vue';

export default {
  components: {
    Input
  },
  data() {
    return {
      foglalasok: []
    }
  },
  methods: {
    foglalaskuld(p) {
      this.foglalasok.push(p);
      console.log(this.foglalasok);
    }
  }

}
</script>

<template>
  <div class="container">
    <Input @foglalaskuld="foglalaskuld" />
  </div>
</template>

<style scoped></style>
