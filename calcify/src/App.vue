<template>
  <v-app class="app-container" :style="{ backgroundPosition: `${mouseX}px ${mouseY}px` }" @mousemove="handleMouseMove">
    <div class="calculator-wrapper">

      <div class="w-full rounded m-1 p-3 text-end lead fw-bold text-white bg-vue-dark">
      {{ calcVal || 0}}
      </div>

      <div class="row g-0">
      <div class="col-3" v-for="btn in calcBtns" :key="btn">
        <div 
        class="lead text-white text-center m-1 py-3 bg-vue-dark rounded btn-hover"
        :class="{'bg-vue-green': ['C', '*', '/', '+', '-', '=', '%'].includes(btn)}"
        @click="action(btn)"
          >
          {{ btn }}
        </div>
      </div>
    </div>

      <!-- <v-container fluid class="calculator">
        <v-row justify="center">
          <div class="text-field-container">
            <v-text-field v-model="myNumber" label="Enter number" hide-details outlined type="number" hide-spin-buttons :class="['text-field']"></v-text-field>
          </div>
          <v-spacer></v-spacer>
        </v-row>
        <v-row justify="center">
        <v-cols cols="12" sm="8" md="6" style="">
          <v-btn variant="outlined" color="black" style="background-color: white;border-width: 5px;">AC</v-btn>
          <v-btn variant="outlined" color="black" style="background-color: white;border-width: 5px;">←</v-btn>
          <v-btn variant="outlined" color="black" style="background-color: white;border-width: 5px;">+/-</v-btn>
        </v-cols>
        </v-row>
      <v-row justify="center">
        <v-cols cols="12" sm="8" md="6" style="">
          <v-btn variant="outlined" color="black" style="background-color: white;border-width: 5px;">1</v-btn>
          <v-btn variant="outlined" color="black" style="background-color: white;border-width: 5px;">2</v-btn>
          <v-btn variant="outlined" color="black" style="background-color: white;border-width: 5px;">3</v-btn>
        </v-cols>
        </v-row>
        <v-row justify="center">
        <v-cols cols="12" sm="8" md="6" style="">
          <v-btn variant="outlined" color="black" style="background-color: white;border-width: 5px;">4</v-btn>
          <v-btn variant="outlined" color="black" style="background-color: white;border-width: 5px;">5</v-btn>
          <v-btn variant="outlined" color="black" style="background-color: white;border-width: 5px;">6</v-btn>
        </v-cols>
        </v-row>
        <v-row justify="center">
        <v-cols cols="12" sm="8" md="6" style="">
          <v-btn variant="outlined" color="black" style="background-color: white;border-width: 5px;">7</v-btn>
          <v-btn variant="outlined" color="black" style="background-color: white;border-width: 5px;">8</v-btn>
          <v-btn variant="outlined" color="black" style="background-color: white;border-width: 5px;">9</v-btn>
        </v-cols>
      </v-row>
      <v-row justify="center">
        <v-cols cols="12" sm="8" md="6" style="">
          <v-btn variant="outlined" color="black" style="background-color: white;border-width: 5px;">%</v-btn>
          <v-btn variant="outlined" color="black" style="background-color: white;border-width: 5px;">0</v-btn>
          <v-btn variant="outlined" color="black" style="background-color: white;border-width: 5px;">.</v-btn>
        </v-cols>
      </v-row>
    </v-container> -->
    </div>
  </v-app>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',

  components: {
    // HelloWorld,
  },

  data() {
    return {
      animateBackground: false,
      mouseX: 0,
      mouseY: 0,
      calcVal: '',
      calcBtns: ['C', '%', '=', '+', 7, 8, 9,'-', 4, 5, 6,'*', 1, 2, 3, '/', 0, '.'],
      operators: null,
      prevCalcVal: '',
    };
  },
  methods: {
    handleMouseMove(event) {
      // Update the mouse cursor coordinates
      this.mouseX = event.clientX*-1/60;
      this.mouseY = event.clientY*-1/60;

      // Activate the animation class
      this.animateBackground = true;
    }
  }
}
</script>

<style scoped>

.btn-hover:hover{
  cursor: pointer;
  background: #3D5875;
}

.app-container {
    background-image: url('./assets/bg.svg');
    background-size: 130%, 130%;
    background-position: center center;
    overflow: hidden;
  }

.app-container.animateBackground{
  transition: 3s;
}

.calculator-wrapper{
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: white;
  height: max-content;
  width: max-content;
  align-self: center;
}

.text-field-container{
  border-radius: px;
}
</style>
