<script setup>
  import {ref, computed} from 'vue'
  import Header from './components/Header.vue'
  import Balance from './components/Balance.vue'
  import IncomeExpenses from './components/IncomeExpenses.vue';
  import AddTransaction from './components/AddTransaction.vue';
  const transactions = ref([])
  // const transactions = ref([
  //   {id: 1, text: 'Flowers', amount: -19.99},
  //   {id: 2, text: 'Salary', amount: 299.99},
  //   {id: 3, text: 'Book', amount: -25.99},
  //   {id: 4, text: 'Camera', amount: 250},
  // ])

  //get total 
  const total = computed(() => {
    return transactions.value.reduce( (acc, transaction) => {
      return acc + transaction.amount
    }, 0)
  })

  //get income
  const income = computed(() => {
    return transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce( (acc, transaction) => {
      return acc + transaction.amount
    }, 0)
    .toFixed(2)
  })


  //get expense
  const expense = computed(() => {
    return transactions.value
    .filter((transaction) => transaction.amount < 0)
    .reduce( (acc, transaction) => {
      return acc + transaction.amount
    }, 0)
    .toFixed(2)
  })

  const handleTransactionSubmitted = (transactionData) => {
    transactions.value.push({
      text: transactionData.text,
      amount: transactionData.amount,
    })
  }
</script>

<template>
  <Header />
  <div class="container">
    <Balance :total="+total"></Balance>
    <IncomeExpenses :income="+income" :expense="+expense"></IncomeExpenses>
    <AddTransaction @transactionSubmitted="handleTransactionSubmitted"></AddTransaction>
    <!-- {{ transactions }} -->
  </div>
</template>