<script>
	// @ts-nocheck

	export let post;
	export let picNumber;

	const fullPath = post.fullPath;
	const segments = fullPath.split('\\'); // Divida a string com base na barra invertida para obter os segmentos do caminho
	const lastSegment = segments[segments.length - 2]; // Pegue o penúltimo segmento, que é o que você deseja
	const route = lastSegment.split('.')[0]; // Remova a extensão do arquivo (segundo-post.md)

	console.log(route);
	// Extrair os dados do artigo

	const { title, author, description, publishedAtIso, imageUrl } = post;
	console.log(title);
	console.log(imageUrl);
</script>

<article
	class="flex flex-col shadow my-4 hover:shadow-lg hover:-translate-y-1 transition-all duration-300 w-full"
>
	<!-- Imagem do Artigo -->
	<!-- svelte-ignore a11y-invalid-attribute -->
	<a href="#" class="w-full">
		<!-- svelte-ignore a11y-missing-attribute -->
		<img src={imageUrl} class="hover:opacity-75 w-full h-96 object-cover" />
	</a>
	<div class="bg-white flex flex-col justify-start p-6">
		<!-- svelte-ignore missing-declaration -->
		<!-- svelte-ignore a11y-invalid-attribute -->
		<!-- <a href="#" class="text-blue-700 text-sm font-bold uppercase pb-4">{category}</a> -->
		<!-- svelte-ignore a11y-invalid-attribute -->
		<a href="#" class="text-3xl font-bold hover:text-gray-700 pb-4">{title}</a>
		<p href="#" class="text-sm pb-3">
			<!-- svelte-ignore a11y-invalid-attribute -->
			By <a href="#" class="font-semibold hover:text-gray-800">{author}</a>, Published at {publishedAtIso}
		</p>
		<p href="#" class="pb-6">{description}</p>
		<!-- svelte-ignore a11y-invalid-attribute -->
		<a href={`/posts/${route}`} class="uppercase text-gray-800 hover:text-black">
			Keep Reading <i class="fas fa-arrow-right"></i>
		</a>
	</div>
</article>
