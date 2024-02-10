<script lang="ts">
	import { goto } from '$app/navigation';

	let title: string = '';
	let author: string = '';
	let description: string = '';
	let genreId: number = 0;
	let pageCount: number = 0;
	let state: string = '';

	const handleSubmit = async () => {
		try {
			const response = await fetch('http://localhost:5000/api/books', {
				method: 'POST',
				headers: {
					'Content-Type': 'application/json'
				},
				body: JSON.stringify({
					title,
					author,
					description,
					genreId,
					pageCount,
					state
				})
			});

			if (!response.ok) {
				throw new Error('Failed to add book');
			}

			const newBook = await response.json();
			console.log('New book created:', newBook);
			goto('/');
		} catch (error) {
			console.error('Error creating book:', error);
		}
	};
</script>

<div class="hero min-h-screen bg-base-200">
	<div class="hero-content flex-col lg:flex-row-reverse">
		<div class="text-center lg:text-left">
			<h1 class="text-5xl font-bold">Add a new book</h1>
			<p class="py-6">Insert the information of the book and click on "Add book"</p>
		</div>
		<div class="card shrink-0 w-full max-w-sm shadow-2xl bg-base-100">
			<form class="card-body" on:submit|preventDefault={handleSubmit}>
				<div class="form-control">
					<label class="label">
						<span class="label-text">Title</span>
					</label>
					<input
						type="text"
						placeholder="title"
						class="input input-bordered"
						bind:value={title}
						required
					/>
				</div>
				<div class="form-control">
					<label class="label">
						<span class="label-text">Author</span>
					</label>
					<input
						type="text"
						placeholder="author"
						class="input input-bordered"
						bind:value={author}
						required
					/>
				</div>
				<div class="form-control">
					<label class="label">
						<span class="label-text">Description</span>
					</label>
					<input
						type="text"
						placeholder="description"
						class="input input-bordered"
						bind:value={description}
						required
					/>
				</div>
				<div class="form-control">
					<label class="label">
						<span class="label-text">Genre</span>
					</label>
					<input
						type="number"
						placeholder="genre"
						class="input input-bordered"
						bind:value={genreId}
						required
					/>
				</div>
				<div class="form-control">
					<label class="label">
						<span class="label-text">Page count</span>
					</label>
					<input
						type="number"
						placeholder="page count"
						class="input input-bordered"
						bind:value={pageCount}
						required
					/>
				</div>
				<div class="form-control">
					<label class="label">
						<span class="label-text">State</span>
					</label>
					<input
						type="text"
						placeholder="state"
						class="input input-bordered"
						bind:value={state}
						required
					/>
				</div>
				<div class="form-control mt-6">
					<button class="btn btn-info" type="submit">Add book</button>
				</div>
			</form>
		</div>
	</div>
</div>
