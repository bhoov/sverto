<script>
  // let's borrow svelte's fly transitions for the circles that need to be
  // created or destroyed
  // https://svelte.dev/tutorial/transition
  import { fly } from "svelte/transition";

  // here we declare `data` as a prop that this component can expect. it has
  // a default value in case we don't provide anything
  // https://svelte.dev/tutorial/declaring-props
  export let data = [5, 15, 10, 12, 14];

  // prefix a statement with $: to make it reactive (so it runs every time
  // data changes)
  // https://svelte.dev/tutorial/reactive-statements
  $: console.log("Dataset prop:", data);

</script>

<!-- we use svelte's in/out transitions for entering and exiting dom elements,
     and vanilla css transitions for retained elements that change. the
     #each block means we create an svg <circle> for each element of data -->
<svg>
  {#each data as d, i (i)}
    <circle
      in:fly="{{y: 100}}" out:fly="{{y: 100}}"
      style={"transition: all 1s ease-out"}
      cx={(15 * i + 10) + "%"} cy="50%" r={d}
      fill="black"
       />
  {/each}
</svg>
