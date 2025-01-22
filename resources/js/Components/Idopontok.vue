<script>
export default {
  props: {
    occupiedTimes: {
      type: Array,
      default: () => []
    },
    selectedTimes: {
      type: Array,
      default: () => []
    },
    currentUser: {
      type: String,
      required: true
    }
  },
  methods: {
    selectTime(time) {
      if (
        this.occupiedTimes.some(
          t => t.ido === time && t.nev === this.currentUser
        )
      ) {
        return; // Prevent re-selecting the same time for the current user
      }
      this.$emit("idokuld", time);
    }
  }
};
</script>

<template>
  <div class="text-center" v-for="i in 9" :key="i">
    <input
      type="button"
      class="btn w-50 my-1"
      :class="{
        'btn-danger': occupiedTimes.some(t => t.ido === i + 7 + ':00:00' && t.nev !== currentUser),
        'btn-warning': occupiedTimes.some(t => t.ido === i + 7 + ':00:00' && t.nev === currentUser),
        'btn-success': !occupiedTimes.some(t => t.ido === i + 7 + ':00:00')
      }"
      :value="i + 7 + ':00'"
      @click="selectTime(i + 7 + ':00:00')"
    />
  </div>
</template>

<style scoped></style>
