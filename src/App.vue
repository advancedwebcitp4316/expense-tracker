<script setup>
  import {ref, computed} from 'vue'
  import Header from './components/Header.vue'
  import Balance from './components/Balance.vue'

  //const transactions = ref([])
  const transactions = ref([
    {id: 1, text: 'Flowers', amount: -19.99},
    {id: 2, text: 'Salary', amount: 299.99},
    {id: 3, text: 'Book', amount: -25.99},
    {id: 4, text: 'Camera', amount: 250},
  ])

  //get total 
  const total = computed(() => {
    return transactions.value.reduce( (acc, transaction) => {
      return acc + transaction.amount
    }, 0)
  })

</script>

<template>
  <Header />
  <div class="container">
    <Balance :total="total"/>
  </div>
</template>