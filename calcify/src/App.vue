<template>
  <v-app class="app-container" :style="{ backgroundPosition: `${mouseX}px ${mouseY}px` }" @mousemove="handleMouseMove">
    <div class="header" style="display: flex; align-items: center; justify-content: center;">
  <v-img src="./assets/calciFyLogo.png" contain max-height="70" max-width="70" style="margin-top: 10px;"></v-img>
  <h1 style="position: relative; color: white; text-align: center; margin-top: 20px;stroke: black;stroke-width: 2px;">𝓒𝓪𝓵𝓬𝓲𝓕𝔂</h1>
</div>
    <div class="container" style="display: flex;">
      <div class="calculator" style="display: flex;">
  <div class="button-container">
  <div :class="['w-full', 'm-1', 'p-3', 'text-end', 'lead', 'fw-bold', 'text-white', 'bg-vue-dark',  {'error-shake': showError }]" style="height: 60px; margin-bottom: 20px;margin-top: 10px;flex-basis: 87.5%;font-size: 20px;border: solid 2px grey; border-radius: 15px;background-color: rgb(228, 225, 225);">
    <h6 class="expression" style="color: rgb(68, 66, 66);margin-right: 5px;overflow: hidden;">{{ expression || null }}</h6>
    <h3 class="input" style="margin-right: 5px;color: black;overflow: hidden;">{{ calcVal || 0 }}</h3>
  </div>
    <div class="button" v-for="btn in calcBtns" :key="btn">
      <div
        class="lead text-white text-center m-1 py-3 bg-vue-dark rounded btn-hover"
        :class="{'bg-vue-green': ['C', '*', '/', '+', '-','←', '%', '='].includes(btn)}"
        @click="action(btn)" style="height: 100%;"
      >
        {{ btn }}
      </div>
    </div>
    <!-- <div class="lead text-center m-1 py-3 bg-vue-dark rounded btn-hover button" style="color: #31475e;"></div>
    <div class="lead text-center m-1 py-3 bg-vue-dark rounded btn-hover button" style="color: #31475e;"></div> -->
  </div>
      </div>
      <footer class="footer">
  <div class="footer-content">
    <h4 style="color:#0d1925">.....</h4>
    <div class="textContainer" style="display: inline-flex;">
      <p class="footerText">Made by</p>
      <h4 style="color:#0d1925">..</h4>
    <p class="footer-text" @click="goToGithubProfile">𝓡𝓸𝓱𝓲𝓽 𝓚𝓚</p>
    </div>
    <i class="fab fa-github" @click="goToGithubRepo"></i>
  </div>
</footer>
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
      mouseX: 0,
      mouseY: 0,
      calcVal: '',
      calcBtns: ['C', '%', '+', '←', 7, 8, 9,'-', 4, 5, 6,'*', 1, 2, 3, '/', 0, '.', '', '='],
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
      this.removeShakeAnimation()
      try{
        if(this.calcVal != '🤦‍♂️'){
          this.removeShakeAnimation()
        }
        if(btn == '←'){
          if(this.calcVal != ''){
            if(this.calcVal == '🤦‍♂️'){
              this.calcVal = '';
              this.expression = '';
            }
            else{
              this.calcVal = this.calcVal.slice(0, -1);
            }
          }
          else{
            this.addShakeAnimation()
          }
        }
        if(!isNaN(btn) || btn === '.')
      {
        if(this.calcVal == '🤦‍♂️' || this.calcVal == ''){
          this.calcVal = btn +''
        }else{
          this.calcVal += btn +''
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
        this.expression += this.calcVal
          this.calcVal = eval(
            this.prevCalcVal + this.operators + this.calcVal
            )
          this.prevCalcVal = ''
          this.operators = null
      }}
      catch(error){
        this.addShakeAnimation()
        this.calcVal="🤦‍♂️"
        this.expression = '*ERROR*'
      }
    },
    handleMouseMove(event) {
      // Update the mouse cursor coordinates
      this.mouseX = event.clientX*-1/60;
      this.mouseY = event.clientY*-1/60;
    },
    goToGithubProfile(){
      window.open("https://github.com/Rohit-KK15", "_blank")
    },
    goToGithubRepo(){
      window.open("https://github.com/Rohit-KK15/Calcify", "_blank")
    },
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
  max-width: 500px;
  width: 100%;
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
  position: fixed;
  bottom: 0;
  width: 100%;
}

.footer-content {
  display: flex;
  justify-content: space-between;
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

}

.fa-github{
  color: aliceblue;
  cursor: pointer;
  font-size: 30px;
  transition: transform 0.3s ease;
}

.fa-github:hover{
  transform: translateY(-3px);
}

@media screen and (max-width: 768px) {
  .calculator {
  margin: 10px;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  width: 100%; /* Adjusted width to be responsive */
  max-width: 500px; /* Added a max-width for larger screens */
  margin: 160px auto;
  background-color: #234;
  border-radius: 10px;
}

.button-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center; /* Modified to center the buttons */
  gap: 5px;
  margin-top: 20px;
  margin-bottom: 20px;
}

.button {
  flex-basis: 21%;
  box-sizing: border-box;
}

.p-3 {
  width: 100%; /* Adjusted width to be responsive */
  max-width: 500px; /* Added a max-width for larger screens */
  background-color: #234;
  border-radius: 10px;
}

.error-shake {
  animation: shake 0.2s;
  animation-iteration-count: 2;
}
  /* Styles for screens up to 768px width (e.g., tablets and smaller screens) */
  .calculator { /* Adjusted width to be full-width */
    max-width: 300px; /* Removed max-width */
    margin: 100px auto; /* Adjusted margin */
  }

  .button-container {
    justify-content: center; /* Center the buttons */
    margin-left: 0; /* Remove the left margin */
    margin-right: 0; /* Remove the right margin */
    margin-top: 10px; /* Adjust the top margin */
    margin-bottom: 10px; /* Adjust the bottom margin */
    display: flex;
    flex-wrap: wrap;
    gap: 5px;
}
.button {
  flex-basis: 21%;
  box-sizing: border-box;
}
}
</style>
