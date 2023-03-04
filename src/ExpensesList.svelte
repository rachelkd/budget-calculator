<script>
    import SectionTitle from "./Title.svelte";
    import Expense from "./Expense.svelte";
    export let expenses = [];
</script>

<style>
    h2 {
        text-transform: capitalize;
    }
</style>

<section>
    <SectionTitle title="Expense list"/>
    <ul>
		{#each expenses as expense}
			<Expense {...expense} />
            {:else}
            <h2>No expenses added to the list!</h2> 
		{/each}
	</ul>
</section>