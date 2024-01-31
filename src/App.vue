<script setup>
  import Header from './components/Header.vue';
  import Balance from './components/Balance.vue';
  import IncomeExpenses from './components/IncomeExpenses.vue';
  import AddTransaction from './components/AddTransaction.vue';
  import {ref, computed} from 'vue'

  const transactions = ref([])

  // const transactions = ref([
  //   {id: 1, text: 'Paycheck', amount: 699.99},
  //   {id: 2, text: 'Food', amount: -35},
  //   {id: 3, text: 'Cat Treats', amount: -25},
  //   {id: 4, text: 'Bill', amount:-200},
  //   {id: 5, text: 'Tigers Vet', amount:-80},
  // ])

  //get total
  const total = computed(() => {
    return transactions.value.reduce( (acc, transaction) => {
      return acc + transaction.amount
    }, 0)
  })

  //get the income by adding positive values
  const income = computed( () => {
    return transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount
    }, 0)
  })

// get the expense by adding all negative values
  const expense = computed( () => {
    return transactions.value
    .filter((transaction) => transaction.amount < 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount
    }, 0)
  })

//handle transaction submitted
  const handleTransactionSubmitted = (transactionData) => {
    transactions.value.push({
      text: transactionData.text,
      amount: transactionData.amount,
    })
  }

</script>

<template>
  <Header></Header>
  <div class="container">
    <Balance :total="total"></Balance> 
    <IncomeExpenses :income="income" :expense="expense"></IncomeExpenses>
    <AddTransaction @transactionSubmitted="handleTransactionSubmitted"></AddTransaction>
    <!-- {{ transactions }} -->
  </div>


</template>