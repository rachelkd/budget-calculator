<script>
    import SectionTitle from "./Title.svelte";
    import Expense from "./Expense.svelte";
    import { fly } from "svelte/transition";
    import { flip  } from "svelte/animate";
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
		{#each expenses as expense, index (expense.id)}
            <div in:fly = {{ x: 200, delay: index*308 }} out:fly = {{ x: -200, delay: index*308 }} animate:flip >
                <Expense {...expense} />
            </div>
            {:else}
            <h2>No expenses added to the list!</h2> 
		{/each}
	</ul>
</section>