<script>
	// @ts-nocheck

	import ArticleCard from '../lib/components/Card.svelte';
	import CardList from '../lib/components/CardList.svelte';
	export let data;

	// -- variável de estado para a página atual
	$: actualPage = 1;
	const postsPerPage = 2;
	$: postsActualPage = [];

	$: {
		const { start, end } = calcularIndices(actualPage);
		console.log('aqui');
		postsActualPage = data.posts.slice(start, end);
		console.log(postsActualPage);
	}

	// -- Função para calcular o índice inicial e final dos posts a serem exibidos
	function calcularIndices(actualPage) {
		const start = (actualPage - 1) * postsPerPage;
		const end = start + postsPerPage;
		return { start, end };
	}

	// -- Method to return total pages
	function getTotalPages() {
		return Math.ceil(data.posts.length / postsPerPage);
	}

	// -- advance pagina
	function nextPage() {
		const totalPages = Math.ceil(data.posts.length / postsPerPage);
		actualPage = actualPage < totalPages ? actualPage + 1 : actualPage;
	}

	// -- return page
	function returnPage() {
		actualPage = actualPage > 1 ? actualPage - 1 : 1;
	}

	function selectPage(pageNumber) {
		console.log('entrei' + pageNumber);
		actualPage = pageNumber;
	}
</script>

<body class="bg-white font-family-karla">
	<!-- Top Bar Nav -->
	<div class="bg-white flex flex-col items-center">
		<a class="flex items-center justify-center" href="#">
			<img src="/BlogKit_logo.png" alt="Logo" class="w-88 h-28" />
		</a>
	</div>

	<nav class="w-full border-t border-b bg-gray-100">
		<div class="w-full flex-grow sm:flex sm:items-center sm:w-auto">
			<div
				class="w-full container mx-auto flex flex-col sm:flex-row items-center justify-center text-sm font-bold uppercase mt-0 px-6 py-2"
			>
				<a href="#" class="hover:bg-gray-400 rounded py-2 px-4 mx-2">Category 1</a>
				<a href="#" class="hover:bg-gray-400 rounded py-2 px-4 mx-2">Category 2</a>
				<a href="#" class="hover:bg-gray-400 rounded py-2 px-4 mx-2">Category 3</a>
				<a href="#" class="hover:bg-gray-400 rounded py-2 px-4 mx-2">Category 4</a>
				<a href="#" class="hover:bg-gray-400 rounded py-2 px-4 mx-2">Category 5</a>
			</div>
		</div>
	</nav>

	<div class="relative bg-gray-100 flex items-center justify-center mb-2 p-6 h-96">
		<!-- Background Image -->
		<div class="absolute inset-0 z-0">
			<img
				src="/from_cool_backgrounds_io.png"
				alt=""
				class="w-full h-full object-cover"
				style="object-fit: cover;"
			/>
		</div>
	</div>

	<!-- Topic Nav -->

	<div class="container bg-white shadow-xl mx-auto flex flex-wrap py-6 px-2">
		<!-- Posts Section -->

		<section class="w-full md:w-2/3 flex flex-col items-center px-3">
			{#if postsPerPage !== undefined}
				{#each postsActualPage as post (post.title)}
					<ArticleCard {post} />
				{/each}
			{/if}
			<!-- Pagination -->
			<div class="flex items-center py-8">
				{#each Array.from({ length: getTotalPages() }) as _, i}
					<button
						on:click={() => selectPage(i + 1)}
						class="h-10 w-10 bg-zinc-600 hover:bg-emerald-600 font-semibold text-white text-sm flex items-center justify-center"
						>{i + 1}</button
					>
				{/each}
			</div>
		</section>

		<!-- Sidebar Section -->

		<aside class="w-full md:w-1/3 flex flex-col items-center px-3 bg-zinc-100 shadow-md">
			<div class="w-full flex flex-col my-4 p-6">
				<CardList />
			</div>
		</aside>
	</div>

	<footer class="w-full border-t bg-white pb-12">
		<div class="relative w-full flex items-center invisible md:visible md:pb-12">
			<button
				on:click={returnPage}
				class="absolute bg-zinc-600 hover:bg-emerald-600 text-white text-2xl font-bold hover:shadow rounded-full w-16 h-16 ml-12"
			>
				&#8592;
			</button>
			<template>
				<img class="w-1/6 hover:opacity-75" />
			</template>
			<button
				on:click={nextPage}
				class="absolute right-0 bg-zinc-600 hover:bg-emerald-600 text-white text-2xl font-bold hover:shadow rounded-full w-16 h-16 mr-12"
			>
				&#8594;
			</button>
		</div>
		<div class="w-full container mx-auto flex flex-col items-center">
			<div class="flex flex-col md:flex-row text-center md:text-left md:justify-between py-6">
				<a href="#" class="uppercase px-3">About Us</a>
				<a href="#" class="uppercase px-3">Privacy Policy</a>
				<a href="#" class="uppercase px-3">Terms & Conditions</a>
				<a href="#" class="uppercase px-3">Contact Us</a>
			</div>
			<div class="uppercase pb-6">&copy; BlogKit</div>
		</div>
	</footer>
</body>
