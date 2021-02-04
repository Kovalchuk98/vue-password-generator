<template>
  <v-container>
    <v-row class="d-flex justify-center mt-sm-4">
      <v-col class="col-sm-6" style="border: 1px solid black;">
        <form action="">
           <v-text-field
            label="Password"
            readonly
            solo
            v-model="passwordValue"
          ></v-text-field>
          <v-btn class="primary" @click="generatePassword">
            Generate Password
          </v-btn>
          <v-row class="my-3 px-4">
            <v-slider
              label="Length"
              min="4"
              max="30"
              step="2"
              hide-details
              ticks
              v-model="passLength"
            >
           </v-slider>
           <span class="ml-2">{{ passLength }}</span>
          </v-row>
           
          <v-switch
            class="switch mt-5"
            v-model="switch1"
            label="Uppercase letters"
          >
          </v-switch>
          <v-switch
            class="switch"
            v-model="switch2"
            label="Lowercase letters"
          >
          </v-switch>
          <v-switch
            class="switch"
            v-model="switch3"
            label="Numbers"
          >
          </v-switch>
          <v-switch
            class="switch"
            v-model="switch4"
            label="Symbols"
          >
          </v-switch>
        </form>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
  export default {
    data: () => ({
      passwordValue: "",
      switch1 : true,
      switch2 : true,
      switch3 : true,
      switch4 : false,
      passLength: 6
    }),
    methods: {
      generatePassword () {
        const UCase = ['A','B','C','D','E','F','G','H','I','J','K','L','M','N','O','P','Q','R','S','T','U','V','W','X','Y','Z']
        const LCase = ['a','b','c','d','e','f','g','h','i','j','k','l','m','n','o','p','q','r','s','t','u','v','w','x','y','z']
        const NumbersArray = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
        const SymbolsArray = ['!','@','#','$','%','^','&','*','(',')','_','+','=','-']
        let password = ""
        let length = this.passLength
        let sw1 = this.switch1
        let sw2 = this.switch2
        let sw3 = this.switch3
        let sw4 = this.switch4

        function getUppercase () {
          return UCase[Math.floor(Math.random() * UCase.length)];
        }

        function getLowercase () {
          return LCase[Math.floor(Math.random() * LCase.length)];
        }
        function getNumber () {
          return NumbersArray[Math.floor(Math.random() * NumbersArray.length)];
        }

        function getSymbol () {
          return SymbolsArray[Math.floor(Math.random() * SymbolsArray.length)];
        }

        for (let i = 0; i <= length; i++) {
          let x = generateChart()
          password += x
        }

        this.passwordValue = password

        function generateChart () {
          
          const xCharts = []
          if (sw1) {
            xCharts.push(getUppercase())
          }
           if (sw2) {
            xCharts.push(getLowercase())
          }
           if (sw3) {
            xCharts.push(getNumber())
          }
           if (sw4) {
            xCharts.push(getSymbol())
          }
          return xCharts[Math.floor(Math.random() * xCharts.length)]
        }
      }
    }
  }
</script>

<style lang="scss">
  .switch {
    padding: 0 !important;
    margin: 0 !important;
  }
</style>
