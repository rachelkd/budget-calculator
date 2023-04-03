<script>
	import {setContext, onMount, afterUpdate } from 'svelte';
	// Components
	import NavBar from "./NavBar.svelte";
	import ExpensesList from "./ExpensesList.svelte";
	import Totals from "./Totals.svelte";
	import ExpenseForm from "./ExpenseForm.svelte";
	import Modal from "./Modal.svelte";
	import Github from "./Github.svelte";
	// Data
	// import expensesData from "./expenses";
	// Variables
	// let expenses = [...expensesData];
	let expenses = [];
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

	// Local Storage
	function setLocalStorage() {
		localStorage.setItem("expenses", JSON.stringify(expenses));
	}
	onMount( () => {
		expenses = localStorage.getItem("expenses") ? JSON.parse(localStorage.getItem("expenses")) : [];
	} )
	afterUpdate( () => {
		console.log("after update");
		setLocalStorage();
	})
</script>

<NavBar {showForm}/>
<main class="content">
	<Github />
	<!-- {#if isFormOpen}
	<Modal>
		<ExpenseForm 
		{addExpense} 
		name = {setName} 
		amount = {setAmount} 
		{isEditing} 
		{editExpense} 
		{hideForm}/>
	</Modal>
		
	{/if}
	<Totals title = "Total expenses" total = {total}/>
	<ExpensesList {expenses} />
	<button type="button" class = "btn btn-primary btn-block" on:click={clearExpenses}>
		Clear expenses
	</button> -->
</main>
