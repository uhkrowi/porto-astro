---
layout: "../../layouts/BlogPost.astro"
title: "Svelte, a promising javascript framework"
pubDate: "Jan 6, 2023"
---

Svelte is a quite popular javascript framework, its documentation can be found at its [official websites](https://svelte.dev/).  
In the first impression, you'll find it pretty simple to work with and easier than other popular frameworks/libraries out there such as React, Vue or Angular.  
Svelte manages a component in a single file, similiar to SFC of Vue, which is one file of `.svelte` equals to one component, and each styling is scoped to its own component.

These are some code examples with svelte.

**reactivity**
```html
<script>
    let count = 0
    
    // every variable in this block changes, this expression will be invoked
    $: console.log('count is ', count)
    
    // if you have multiple lines of block, just wrap 'em in brackets
    <!--$: {-->
    <!--    console.log('log: count is ', count)-->
    <!--    console.log('log: count is ', count)-->
    <!--}-->
    
    function incrementCount() {
        count++
    }
</script>

<button type="button" on:click={incrementCount}>
  Increment count
</button>
```
In case you curious about the `$:`, you can find out its explanation [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/label).

**if, else if, else**
```html
<script>
    const gender = 'male'
</script>

{#if gender == 'male'}
  <p>It's a boy!</p>
{:else if gender == 'female'}
  <p>It's a girl!</p>
{:else}
  <p>We don't know yet.</p>
{/if}
```
Symbol `#` is used to begin an expression.
Symbol `:` is used to continue its expression block.
And the last, symbol `/` is used to end an expression.

**iterating**:
```html
<script>
    const members = [
        {id: 1, name: 'Arul'},
        {id: 2, name: 'Budi'},
        {id: 3, name: 'John'}
    ]
</script>

{#each members as {id, name}, i (i)}
  <p>{i+1}. {name} has ID: {id}</p>
{/each}
```
You can do destructuring the every object of `members` with `{id, name}`. 
Notice there is `(i)`, it means you're assigning the i (index) as the key of each DOM node that iterated in `each` expression.

**nested component**  
Child.svelte
```html
<script>
    export let name = 'User'
</script>

<p>Hello {name}!</p>
```

Parent.svelte
```html
<script>
    import Child from './Child.svelte'
    
    const name = 'Arul'
</script>

<Child {name} />
<Child />
```
As we can see that `Child.svelte` component can retrieve the prop `name`, but it has a default value, so we can leave it not set in `Parent.svelte` component. 