<script>
	import {setContext} from 'svelte';
	// Components
	import NavBar from "./NavBar.svelte";
	import ExpensesList from "./ExpensesList.svelte";
	import Totals from "./Totals.svelte";
	import ExpenseForm from "./ExpenseForm.svelte";
	// Data
	import expensesData from "./expenses";
	// Variables
	let expenses = [...expensesData];
	// Reactive
	$: total = expenses.reduce((acc,curr)=>{
		// console.log({acc,amount:curr.amount});
		return (acc += curr.amount)
	},0);
	console.log(expenses);
	// Functions
	function removeExpense(id){
		expenses = expenses.filter(item => item.id !== id);
	}
	function clearExpenses() {
		expenses = [];
	}
	// Context
	setContext("remove", removeExpense);
</script>

<NavBar />
<main class="content">
	<ExpenseForm />
	<Totals title = "Total expenses" total = {total}/>
	<ExpensesList {expenses} />
	<button type="button" class = "btn btn-primary btn-block" on:click={clearExpenses}>
		Clear expenses
	</button>
</main>