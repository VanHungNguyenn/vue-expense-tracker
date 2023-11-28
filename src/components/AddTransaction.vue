<template>
	<h3>Add new transaction</h3>
	<form action="" id="form">
		<div class="form-control">
			<label for="text">Text</label>
			<input
				type="text"
				name="text"
				id="text"
				placeholder="Enter text..."
			/>
		</div>
		<div class="form-control">
			<label for="amount">
				Amount <br />
				(negative - expense, positive - income)
			</label>
			<input
				type="number"
				name="amount"
				id="amount"
				placeholder="Enter amount..."
			/>
		</div>
		<button class="btn">Add transaction</button>
	</form>
</template>

<script setup></script>

<style scoped></style>
