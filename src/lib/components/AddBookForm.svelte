<!-- AddBookForm.svelte -->
<script lang="ts">
  import { createEventDispatcher } from 'svelte';
  
  let title: string = '';
  let author: string = '';
  let description: string = '';
  let genre: string = '';
  let pageCount: string = '';
  let state: string = '';
  
  const dispatch = createEventDispatcher();
  
  const handleSubmit = () => {
      title,
      author,
      description,
      genre,
      pageCount,
      state,
    };
    
    dispatch('submit', formData);
  };
</script>

<form on:submit|preventDefault={handleSubmit}>
	<input type="text" bind:value={title} placeholder="Title" required />
	<input type="text" bind:value={author} placeholder="Author" required />
	<textarea bind:value={description} placeholder="Description"></textarea>
	<input type="text" bind:value={genre} placeholder="Genre" required />
	<input type="number" bind:value={pageCount} placeholder="Page Count" required />
	<input type="text" bind:value={state} placeholder="State" required />
	<button type="submit">Add Book</button>
</form>
