<svelte:head>
	<title>{post.title}</title>
</svelte:head>

<h1>{post.title}</h1>

<div class="content">
	{@html post.html}
</div>

<script context="module">
	let item = {};

	function load(title) {
		return fetch(`https://sapper-template.now.sh/blog/${title}.json`).then(r => r.json());
	}

	export function preload(req) {
		return load(req.params.title).then(obj => item = obj);
	}
</script>

<script>
	export let params = {};

	let post = item;

	$: if (params.title) load(params.title).then(obj => { post = obj });
</script>

<style>
	.content :global(h2) {
		font-size: 1.4em;
		font-weight: 500;
	}
	.content :global(pre) {
		background-color: #f9f9f9;
		box-shadow: inset 1px 1px 5px rgba(0,0,0,0.05);
		padding: 0.5em;
		border-radius: 2px;
		overflow-x: auto;
	}
	.content :global(pre) :global(code) {
		background-color: transparent;
		padding: 0;
	}
	.content :global(ul) {
		line-height: 1.5;
	}
	.content :global(li) {
		margin: 0 0 0.5em 0;
	}
</style>
