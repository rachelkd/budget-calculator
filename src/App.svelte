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
	// Set editing variables
	let setName = "";
	let setAmount = null;
	let setId = null;
	// Toggle form variables
	let isFormOpen = false;

	// Reactive
	$: isEditing = setId?true:false;
	$: total = expenses.reduce((acc,curr)=>{
		// console.log({acc,amount:curr.amount});
		return (acc += curr.amount)
	},0);
	console.log(expenses);
	// Functions
	function showForm() {
		isFormOpen = true;
	}
	function hideForm() {
		isFormOpen = false;
	}

	function removeExpense(id){
		expenses = expenses.filter(item => item.id !== id);
	}
	function clearExpenses() {
		expenses = [];
	}
	function addExpense({name, amount}) {
		let expense = { id: Math.random() * Date.now(), name, amount};
		expenses = [expense, ...expenses];
	}
	function setModifiedExpense(id) {
		let expense = expenses.find(item => item.id === id);
		setId = expense.id;
		setName = expense.name;
		setAmount = expense.amount;
		showForm();
	}
	function editExpense({name, amount}) {
		expenses = expenses.map(item => {
			return item.id === setId ? { ...item, name, amount }: { ...item }
		});
		setId = null;
		setAmount = null;
		setName = "";
	}
	// Context
	setContext("remove", removeExpense);
	setContext("modify", setModifiedExpense);
</script>

<NavBar {showForm}/>
<main class="content">
	{#if isFormOpen}
		<ExpenseForm {addExpense} name = {setName} amount = {setAmount} {isEditing} {editExpense} {hideForm}/>
	{/if}
	<Totals title = "Total expenses" total = {total}/>
	<ExpensesList {expenses} />
	<button type="button" class = "btn btn-primary btn-block" on:click={clearExpenses}>
		Clear expenses
	</button>
</main>