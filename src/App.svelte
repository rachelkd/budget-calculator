<script>
	import {setContext} from 'svelte';
	// Components
	import NavBar from "./NavBar.svelte";
	import ExpensesList from "./ExpensesList.svelte";
	// Data
	import expensesData from "./expenses";
	// Variables
	let expenses = [...expensesData];
	console.log(expenses);
	// Functions
	function removeExpense(id){
		expenses = expenses.filter(item => item.id !== id);
	}
	// Context
	setContext("remove", removeExpense);
</script>

<NavBar />
<main class="content">
	<ExpensesList {expenses} />
</main>