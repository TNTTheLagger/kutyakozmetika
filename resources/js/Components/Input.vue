<script>
import Idopontok from '../Components/Idopontok.vue';

export default {
  components: {
    Idopontok
  },
  props: {
    occupiedTimes: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      foglalas: {
        nev: "",
        datum: "",
        ido: ""
      },
      selectedTimes: [] // Stores currently selected times
    };
  },
  methods: {
    idokuld(p) {
      // Add or remove selected time
      if (this.selectedTimes.includes(p)) {
        this.selectedTimes = this.selectedTimes.filter(time => time !== p);
      } else {
        this.selectedTimes = [p]; // Allow one selection at a time
        this.foglalas.ido = p;
      }

      // Emit booking if all fields are filled
      if (this.foglalas.nev && this.foglalas.datum) {
        this.$emit("foglalaskuld", { ...this.foglalas });
      }
    },
    calculateColor(percentage) {
      const green = Math.floor(255 * (1 - percentage));
      const red = Math.floor(255 * percentage);
      return `rgb(${red}, ${green}, 0)`;
    }
  },
  computed: {
    showPreview() {
      return !this.foglalas.nev || !this.foglalas.datum;
    },
    previewData() {
      return Object.keys(this.occupiedTimes).map(date => {
        const totalSlots = 9; // Total timeslots per day
        const occupiedSlots = this.occupiedTimes[date]?.length || 0;
        const percentage = occupiedSlots / totalSlots;
        return {
          date,
          color: this.calculateColor(percentage)
        };
      });
    }
  }
};
</script>

<template>
  <div class="card">
    <div class="card-body">
      <h2 class="card-title text-center">Kutyakozmetikus Foglalás</h2>
      <p class="card-text">
        <div class="mb-3">
          <label for="nev" class="form-label">Név</label>
          <input
            type="text"
            class="form-control"
            id="nev"
            v-model="foglalas.nev"
          />
        </div>
        <div class="mb-3">
          <label for="datum" class="form-label">Dátum</label>
          <input
            type="date"
            class="form-control"
            id="datum"
            v-model="foglalas.datum"
          />
        </div>
      </p>
    </div>
    <div v-if="showPreview" class="preview-container">
      <h3>Foglalás előnézet</h3>
      <div class="preview-grid">
        <div
          v-for="day in previewData"
          :key="day.date"
          :style="{ backgroundColor: day.color }"
          class="preview-item"
        >
          {{ day.date }}
        </div>
      </div>
    </div>
    <Idopontok
      v-else
      :occupied-times="occupiedTimes[foglalas.datum] || []"
      :current-user="foglalas.nev"
      :selected-times="selectedTimes"
      @idokuld="idokuld"
    />
  </div>
</template>

<style scoped>
.preview-container {
  margin-top: 20px;
}
.preview-grid {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
}
.preview-item {
  width: 100px;
  height: 100px;
  display: flex;
  justify-content: center;
  align-items: center;
  border: 1px solid #ccc;
  color: #fff;
  font-weight: bold;
}
</style>
