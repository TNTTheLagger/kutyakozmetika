<script>
import Input from '../Components/Input.vue';

export default {
  components: {
    Input
  },
  data() {
    return {
      foglalasok: [], // Stores all bookings
      occupiedTimes: {} // Stores occupied times for each date
    };
  },
  methods: {
    foglalaskuld(p) {
      // Store the booking
      this.foglalasok.push(p);

      // Update occupied times
      if (!this.occupiedTimes[p.datum]) {
        this.occupiedTimes[p.datum] = [];
      }
      this.occupiedTimes[p.datum].push({
        nev: p.nev,
        ido: p.ido
      });

      console.log('Foglalások:', this.foglalasok);
      console.log('Occupied Times:', this.occupiedTimes);
    }
  }
};
</script>

<template>
  <div class="container">
    <Input @foglalaskuld="foglalaskuld" :occupied-times="occupiedTimes" />
  </div>
</template>

<style scoped></style>
