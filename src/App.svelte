<script>
	// Components
	import NavBar from "./NavBar.svelte";
	import ExpensesList from "./ExpensesList.svelte";
	// Data
	import expensesData from "./expenses";
	// Variables
	let expenses = [...expensesData];
	console.log(expenses);
</script>

<NavBar />
<main class="content">
	<ExpensesList {expenses} />
</main>