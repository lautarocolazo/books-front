<script lang="ts">
	import { onMount } from 'svelte';
	import { writable } from 'svelte/store';

	interface Book {
		id: number;
		title: string;
		author: string;
		description: string;
		genre: string;
		pageCount: number;
		state: string;
	}

	const books = writable<Book[]>([]);

	async function fetchBooks(): Promise<void> {
		try {
			const response = await fetch('http://localhost:5000/api/books');
			if (!response.ok) {
				console.log('Failed to retrieve books');
			}
			const data: Book[] = await response.json();
			books.set(data);
		} catch (error) {
			console.error('Error fetching books:', error);
		}
	}

	const deleteBook = async (id: number) => {
		try {
			const response = await fetch(`http://localhost:5000/api/books/${id}`, {
				method: 'DELETE'
			});
			if (!response.ok) {
				console.log('Failed to delete book');
			}
			books.update((existingBooks) => existingBooks.filter((book) => book.id !== id));
		} catch (error) {
			console.error('Error deleting book:', error);
		}
	};

	onMount(fetchBooks);
</script>

<main class="flex-grow">
	<div class="container mx-auto my-4">
		<h1 class="text-6xl font-extrabold text-center my-4">myBooks</h1>
		<div class="grid grid-cols-3 gap-4">
			{#each $books as book}
				<div class="card w-80 bg-neutral text-neutral-content shadow-xl">
					<div class="card-body">
						<h2 class="card-title">{book.title}</h2>
						<p>{book.description}</p>
						<div class="card-actions justify-end">
							<div class="badge badge-outline bg-warning">{book.genre.name}</div>
							<div class="badge badge-outline bg-info">{book.author}</div>
							<div class="badge badge-outline bg-success">{book.state}</div>
							<div class="badge badge-outline bg-neutral">{book.pageCount} pages</div>
						</div>
						<button class="btn btn-xs btn-error w-16" on:click={() => deleteBook(book.id)}
							>Delete</button
						>
					</div>
				</div>
			{/each}
		</div>
	</div>
</main>
