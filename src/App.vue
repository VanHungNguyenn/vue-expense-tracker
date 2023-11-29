<template>
	<Header />
	<div class="container">
		<Balance :total="total" />
		<IncomeExpense :income="+income" :expense="+expense" />
		<TransactionList
			@transactionDeleted="handleTransactionDeleted"
			:transactions="transactions"
		/>
		<AddTransaction @transactionSubmitted="handleTransactionSubmitted" />
	</div>
</template>

<script setup>
import Header from './components/Header.vue'
import Balance from './components/Balance.vue'
import IncomeExpense from './components/IncomeExpense.vue'
import TransactionList from './components/TransactionList.vue'
import AddTransaction from './components/AddTransaction.vue'

import { reactive, computed, onMounted } from 'vue'
import { useToast } from 'vue-toastification'

const toast = useToast()

let transactions = reactive([])

onMounted(() => {
	const savedTransactions = JSON.parse(localStorage.getItem('transactions'))

	if (savedTransactions) {
		transactions.splice(0, transactions.length)

		savedTransactions.forEach((transaction) => {
			transactions.push(transaction)
		})
	}
})

const total = computed(() => {
	return transactions.reduce(
		(acc, transaction) => acc + transaction.amount,
		0
	)
})

const income = computed(() => {
	return transactions
		.filter((transaction) => transaction.amount > 0)
		.reduce((acc, transaction) => acc + transaction.amount, 0)
		.toFixed(2)
})

const expense = computed(() => {
	return transactions
		.filter((transaction) => transaction.amount < 0)
		.reduce((acc, transaction) => acc + transaction.amount, 0)
		.toFixed(2)
})

const handleTransactionSubmitted = (transactionData) => {
	transactions.push({
		id: Math.floor(Math.random() * 100000000),
		text: transactionData.text,
		amount: transactionData.amount,
	})

	saveTransactionsToLocalStorage()

	toast.success('Transaction added')
}

const handleTransactionDeleted = (id) => {
	transactions.splice(
		transactions.findIndex((transaction) => transaction.id === id),
		1
	)

	saveTransactionsToLocalStorage()

	toast.success('Transaction deleted')
}

const saveTransactionsToLocalStorage = () => {
	localStorage.setItem('transactions', JSON.stringify(transactions))
}
</script>

<style scoped></style>
