<script>
	import { fade, fly } from "svelte/transition";
	import Thing from "./components/Thing.svelte";

	let chosen = null;
	let thing = null;
	let things = [];
	$: choosable = things && things.length > 1;
	const addThing = ({ key }) => {
	  if (key === "Enter") {
	    if (!things.includes(thing)) things = [...things, thing];
	    thing = null;
	  }
	};

	const removeThing = index => {
	  const newThings = things.filter((t, i) => i !== index);
	  things = newThings;
	};

	const choose = () => {
	  chosen = things[Math.floor(Math.random() * things.length)];
	  thing = null;
	  things = [];
	};

	const reset = () => {
	  chosen = null;
	};
</script>

<style>
	div.centered {
	  padding: 20px;
	  border: solid 4px white;
	  border-radius: 5px;
	  display: flex;
	  flex-direction: column;
	  align-items: center;
	  justify-content: center;
	  box-shadow: 3px 3px #888888;
	}

	div.list-wrapper {
		margin-bottom: 10px;
	}

	ul.list {
	  padding-inline-start: 0;
	}
	.nothing {
		color: #aaaaaa;
	}
</style>
<div>
{#if !chosen}
<div class="centered">
	<h1>Gimme the things</h1>

	<p>
		<input type="text" placeholder="A thing" bind:value={thing} on:keydown|stopPropagation={addThing}/>
	</p>

	<div class="list-wrapper">
		<h3>Things to choose from</h3>
		<ul class="list">
			{#if !things.length}
				<span class="nothing">Nothing yet</span>
			{/if}
			{#each things as thingy, i}
				<Thing index={i} thing={thingy} onRemove={() => removeThing(i)}/>
			{/each}
		</ul>
	</div>

	<button disabled={!choosable} on:click={choose}>Choose Ammoozzo</button>
</div>
{:else}
	<div in:fade={{duration:1000}} class="centered">
		<h2>I choose, ammoozzo</h2>
		<h1>{chosen}</h1>
		<button in:fly={{x:-400,duration:1000}} on:click={reset}>Reset</button>
	</div>
{/if}
</div>