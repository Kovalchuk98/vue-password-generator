<template>
    <v-row class="d-flex justify-center ma-0 pa-0">
      <v-col class="pass_wrapper col-sm-8 col-md-6 mt-0 mt-sm-4">
        <form action="">
          <div class="d-flex align-center">
            <v-text-field
              ref="textToCopy"
              class="passText px-2 px-sm-0 mt-2"
              label="Password"
              solo
              v-model="passwordValue"
            ></v-text-field>
              <v-tooltip v-model="show" bottom :open-on-hover="false" close-delay="1500">
                <template v-slot:activator="{ on }">
                  <div v-on="on">
                    <v-btn
                    class="ml-2 my-2"
                    color="error"
                    fab
                    x-small
                    @click="copyPassword"
                    @blur="on.blur" 
                    retain-focus-on-click
                  >
                    <v-icon>mdi-content-copy</v-icon>
                  </v-btn>
                  </div>
                </template>
                <span>Copied</span>
              </v-tooltip>

            </div>
            <v-btn class="blue rounded-xl my-2" @click="generatePassword" style="color: #fff;">
              Generate password
            </v-btn>
          <v-row class="my-3 px-4">
            <v-slider
              label="Length"
              min="4"
              max="30"
              step="2"
              color="blue"
              hide-details
              ticks
              v-model="passLength"
            >
           </v-slider>
           <span class="length ml-2">{{ passLength }}</span>
          </v-row>
          <v-col class="settings rounded-lg">
          <v-switch
            class="switch mt-5"
            v-model="switch1"
            color="blue"
            label="Uppercase letters"
          >
          </v-switch>
          <v-switch
            class="switch"
            v-model="switch2"
            color="blue"
            label="Lowercase letters"
          >
          </v-switch>
          <v-switch
            class="switch"
            v-model="switch3"
            color="blue"
            label="Numbers"
          >
          </v-switch>
          <v-switch
            class="switch"
            v-model="switch4"
            color="blue"
            label="Symbols"
          >
          </v-switch>
          </v-col>
        </form>
      </v-col>
    </v-row>
</template>

<script>
  export default {
    data: () => ({
      showTip: false,
      passwordValue: "",
      switch1 : true,
      switch2 : true,
      switch3 : true,
      switch4 : false,
      passLength: 6,
      UCase: ['A','B','C','D','E','F','G','H','I','J','K','L','M','N','O','P','Q','R','S','T','U','V','W','X','Y','Z'],
      LCase: ['a','b','c','d','e','f','g','h','i','j','k','l','m','n','o','p','q','r','s','t','u','v','w','x','y','z'],
      NumbersArray: [0, 1, 2, 3, 4, 5, 6, 7, 8, 9],
      SymbolsArray: ['!','@','#','$','%','^','&','*','(',')','_','+','=','-']
    }),
    methods: {
      copyPassword () {
          let textToCopy = this.$refs.textToCopy.$el.querySelector('input')
          textToCopy.select()
          document.execCommand("copy");
          textToCopy.blur()
      },
      generatePassword () {
       
        let password = ""
        let length = this.passLength

        for (let i = 0; i <= length; i++) {
          let x = this.generateChart()
          password += x
        }
        this.passwordValue = password
      },

       getUppercase () {
          return this.UCase[Math.floor(Math.random() * this.UCase.length)];
        },

         getLowercase () {
          return this.LCase[Math.floor(Math.random() * this.LCase.length)];
        },
         getNumber () {
          return this.NumbersArray[Math.floor(Math.random() * this.NumbersArray.length)];
        },

         getSymbol () {
          return this.SymbolsArray[Math.floor(Math.random() * this.SymbolsArray.length)];
        },
          generateChart () {
          
          const xCharts = []
          if (this.switch1) {
            xCharts.push(this.getUppercase())
          }
           if (this.switch2) {
            xCharts.push(this.getLowercase())
          }
           if (this.switch3) {
            xCharts.push(this.getNumber())
          }
           if (this.switch4) {
            xCharts.push(this.getSymbol())
          }
          if (xCharts.length === 0) return ""

           for (let i = xCharts.length - 1; i > 0; i--) {
              let j = Math.floor(Math.random() * (i + 1));
              [xCharts[i], xCharts[j]] = [xCharts[j], xCharts[i]];
            }
          return xCharts[0]
        }
    }
  }
</script>

<style lang="scss">
  .switch {
    padding: 0 !important;
    margin: 0 !important;
  }
  .pass_wrapper{
    border-radius: .3rem;
    color: #041948 !important;
    background-color: #fff;
    border: 1px solid #fff;
  }
  .v-label {
    color: #041948 !important;
  }
  .length {
    font-weight: bold;
  }
  .v-input__control .v-text-field__details {
    display: none;
  }
  .settings{
    background-color: #f8f8f8;
  }
</style>
