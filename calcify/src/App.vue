<template>
  <v-app class="app-container" :style="{ backgroundPosition: `${mouseX}px ${mouseY}px` }" @mousemove="handleMouseMove">
    <div class="header" style="display: flex; align-items: center; justify-content: center;">
  <v-img src="./assets/calciFyLogo.png" contain max-height="70" max-width="70"></v-img>
  <h1 style="position: relative; color: white; text-align: center; margin-top: 10px;">ⒸⓐⓛⓒⓘⒻⓨ</h1>
</div>
    
    <!-- <div class="p-3"> -->
      <div class="calculator">
  <div class="button-container">
  <div :class="['w-full', 'm-1', 'p-3', 'text-end', 'lead', 'fw-bold', 'text-white', 'bg-vue-dark',  {'error-shake': showError }]" style="height: 60px; margin-bottom: 20px;flex-basis: 87.5%;font-size: 20px;border: solid 2px grey; border-radius: 15px;background-color: rgb(228, 225, 225);">
    <h6 class="expression" style="color: rgb(68, 66, 66);margin-right: 5px;">{{ expression || null }}</h6>
    <h2 class="input" style="margin-right: 5px;color: black;">{{ calcVal || 0 }}</h2>
  </div>
    <div class="button" v-for="btn in calcBtns" :key="btn">
      <div
        class="lead text-white text-center m-1 py-3 bg-vue-dark rounded btn-hover"
        :class="{'bg-vue-green': ['C', '*', '/', '+', '-', '=', '%'].includes(btn)}"
        @click="action(btn)"
      >
        {{ btn }}
      </div>
    </div>
  </div>
      </div>
      <footer class="footer">
  <div class="footer-content">
    <p class="footerText">Made by</p>
    <p class="footer-text">𝓡𝓸𝓱𝓲𝓽 𝓚𝓚</p>
  </div>
</footer>
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
      mouseX: 0,
      mouseY: 0,
      calcVal: '',
      calcBtns: ['C', '%', '=', '+', 7, 8, 9,'-', 4, 5, 6,'*', 1, 2, 3, '/', 'as', 0, '.', 'as'],
      operators: null,
      prevCalcVal: '',
      expression:'',
      showError: false,
    };
  },
  methods: {
    addShakeAnimation() {
      this.showError = true;
    },
    removeShakeAnimation() {
      this.showError = false;
    },
    action(btn){
      try{
        if(this.calcVal != '🤦‍♂️'){
          this.removeShakeAnimation()
        }
        if(!isNaN(btn) || btn === '.')
      {
        if(this.calcVal == '🤦‍♂️'){
          this.calcVal = btn +''
        }else{
          this.calcVal += btn +''
        }
        if(this.expression != ''){
            this.expression += this.calcVal;
          }
      }
      if (btn === 'C') {
        this.calcVal = ''
        this.expression = ''
      }
      if (btn === '%') {
        this.expression += this.calcVal + btn
        this.calcVal = this.calcVal / 100 + ''
      }
      if (['/', '+', '-', '*'].includes(btn)) {
        this.operators = btn
        this.prevCalcVal = this.calcVal
        this.expression += this.calcVal + btn + ''
        this.calcVal = ''
      }
      if (btn === "=") {
          this.calcVal = eval(
            this.prevCalcVal + this.operators + this.calcVal
            )
          this.prevCalcVal = ''
          this.operators = null
      }}
      catch(error){
        this.addShakeAnimation()
        this.calcVal="🤦‍♂️"
        this.expression = ''
      }
    },
    handleMouseMove(event) {
      // Update the mouse cursor coordinates
      this.mouseX = event.clientX*-1/60;
      this.mouseY = event.clientY*-1/60;
    }
  },
}
</script>

<style scoped>

.app-container {
    background-image: url('./assets/bg.svg');
    background-size: 130%, 130%;
    background-position: center center;
    overflow: hidden;
  }


.bg-vue-dark{
  background: #31475e;
}
.btn-hover:hover{
  cursor: pointer;
  background: #3D5875;
}

.bg-vue-green{
  background: #56acac ;
}

.calculator {
  margin: 10px;
  display: flex; 
  flex-wrap: wrap; 
  justify-content: center; 
  width: 500px;
  margin: 160px auto;
  background-color: #234;
  border-radius: 10px;
}

.button-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: flex-start;
  gap: 5px;
  margin-left: 60px;
  margin-top: 20px;
  margin-bottom: 20px;
}

.button {
  flex-basis: 21%;
  box-sizing: border-box;
}

.p-3 {
  width: 500px;
  background-color: #234;
  border-radius: 10px;
}

.error-shake {
  animation: shake 0.2s;
  animation-iteration-count: 2;
}

@keyframes shake {
  0% {
    transform: translateX(0);
  }
  25% {
    transform: translateX(-5px);
  }
  75% {
    transform: translateX(5px);
  }
  100% {
    transform: translateX(0);
  }
}

.footer {
  background-color: #0d1925;
  padding-left: 20px;
  padding-right: 20px;
  text-align: center;
  position: relative;
}

.footer:before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(255, 255, 255, 0.5);
  backdrop-filter: blur(10px);
  z-index: -1;
}

.footer-content {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
  gap: 10px;
}

.footer-text {
  font-size: 25px;
  color: cyan;
  margin: 0;
  cursor: pointer;
  transition: transform 0.3s ease;
}

.footer-text:hover {
  transform: translateY(-3px);
}

.footerText {
  font-size: 20px;
  color: rgb(255, 255, 255);
  margin: 0;
}

</style>