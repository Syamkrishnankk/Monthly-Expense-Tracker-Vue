<template>
  <v-container class="fill-height">
    <v-responsive
      class="align-center fill-height mx-auto"
      max-width="900"
    >
    <h2 align="center" class="mt-n6 mb-10">Monthly Expense Tracker</h2>
    <v-row align="center" justify="center">
      <v-card
      width="500"
      variant="tonal"
      color="indigo"
      >
      <v-card
      color="transparent"
      class="pa-5"
      rounded="0"
      >
      <v-row >
        <v-col justify="center" align="center">
          <h4 style="color: rgba(220, 255, 227, 0.9);" class="mb-2">Monthly Income</h4>
          <h2 style="color: rgb(220, 255, 227);">₹ {{ MonthlyIncome }}</h2>
        </v-col>
        <v-divider vertical :thickness="2" class="border-opacity-25" color="white"></v-divider>
        <v-col justify="center" align="center">
          <h4 style="color: rgba(255, 217, 227, 0.9);" class="mb-2">Monthly Expense</h4>
          <h2 style="color: rgb(255, 217, 227);">₹ {{ MonthlyExpense }}</h2>
        </v-col>
      </v-row>
        
        
      </v-card>
      <v-card
      color="transparent"
      class="pa-5"
      rounded="0"
      >
      <v-row class="mx-15">
        
          <v-radio-group inline color="white" class="mx-10 mt-4" v-model="Selected" >
          <v-radio label="Income" value="Income" style="color: white;" ></v-radio>
          <v-radio label="Expenses" value="Expense" style="color: white;" class="mx-2" ></v-radio>
          </v-radio-group>
        

      </v-row>
      <v-row class="mx-2">
        <v-col cols="10">
          <v-text-field
            v-model="Amount"
            label="Amount"
            type="number"
            variant="outlined"
            clearable
            style="color: white;"
            @keyup.enter="Check"
          >
          </v-text-field>
          
        </v-col>
        <v-col cols="2">
          <v-btn class="mt-2" @click="Check"> Add </v-btn>
        </v-col>
        
      </v-row>
        
        
      </v-card>
      <v-card color="transparent" variant="flat">
      <v-row align="center" class="mx-6 mt-3">
        <h4 style="color: rgb(251, 251, 251); font-weight: 400;" class="mr-2">Balance</h4>
        <h3 style="color: white;">₹ {{ Balance }}</h3>
      </v-row>
        

        
      
      <br />
      <v-card-text>
        <!-- <div
          :style="`right: calc(${review} - 30px )`"
          class="position-absolute mt-n8 text-caption"
        >
        <h4 style="color: rgb(251, 251, 251); font-weight: 400;" class="mr-2 pl-15">Balance</h4>
        </div> -->
        <v-progress-linear
          color="brown-lighten-1"
          height="22"
          :model-value="review"
          rounded="lg"
        >
          <!-- <v-badge
            :style="`right: ${review}`"
            class="position-absolute"
            color="black"
            dot
            inline
          ></v-badge> -->
         
        </v-progress-linear>

        <div class="d-flex justify-space-between py-3">
          <span class="font-weight-medium" style="color: #daaa99;">
            Balance
          </span>

          <span class="font-weight-medium" style="color: rgb(255, 255, 255);"> Total Income </span>
        </div>
      </v-card-text>

      <v-divider></v-divider>
    </v-card>
      </v-card>
    </v-row>
    
     
    </v-responsive>
  </v-container>
</template>

<script setup>
  import { ref } from 'vue'
  const review = ref("0%");
  const MonthlyIncome = ref(0);
  var MonthlyExpense = ref(0);
  var Amount = ref()
  var Balance = ref(0);
  const Selected = ref('')
  
  const Check = () =>{
    console.log(Selected.value)
    if(Selected.value == 'Income'){
      MonthlyIncome.value += Number(Amount.value);
      
    }
    if(Selected.value == 'Expense'){
      // if(MonthlyIncome.value > 0 && MonthlyIncome.value >= MonthlyExpense.value){
        
      // }
      // else{
      //   window.alert('Not enough Money');
      //   Amount.value = ''
      // }
      MonthlyExpense.value += Number(Amount.value);
        
    }
    Balance.value = MonthlyIncome.value-MonthlyExpense.value;
    var percentage;
    percentage = MonthlyExpense.value/MonthlyIncome.value*100;
    review.value = 100-percentage + '%';
    Amount.value = '' 
    Selected.value = ''
    console.log(percentage);
    console.log(review.value)
  }
</script>
