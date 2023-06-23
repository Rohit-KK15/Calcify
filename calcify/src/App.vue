<template>
  <v-app class="app-container" :style="{ backgroundPosition: `${mouseX}px ${mouseY}px` }" @mousemove="handleMouseMove">
    <div class="calculator-wrapper">
      <v-container fluid class="calculator">
        <v-row justify="center">
          <v-text-field class="text-field" rounded v-model="text" placeholder="Give Me Some Problems....."></v-text-field>
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
    </v-container>
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
      mouseY: 0
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
  height: fit-content;
  width: fit-content;
  align-self: center;
}

.text-field{
  border-radius: 20px;
}
</style>
