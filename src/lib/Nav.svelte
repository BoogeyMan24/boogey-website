<script>
	import NavItem from "$lib/NavItem.svelte";

	function scrollTo(id) {
		const section = document.getElementById(id);
		if (!section) return;
		
		section.scrollIntoView({ behavior: "smooth" });
	}
</script>

<nav class="pt-10 pb-12">
	<div class="flex justify-between items-center flex-nowrap">
		<logo>
			<a href="/"><img src="/s/misc/pfp.png" alt="pfp logo" class="aspect-square rounded-full w-10 h-auto"></a>
		</logo>
		<div class="">
			<ul class="">
				<li class="inline ml-12 text-white">
					<button on:click|preventDefault={() => scrollTo("projects")} href="projects" class="hover:border-b-2 hover:animate-[fade_0.1s_ease-in-out]">Projects</button>
				</li>
				<li class="inline ml-12 text-white">
					<a href="about-me" class="hover:border-b-2 hover:animate-[fade_0.1s_ease-in-out]">About Me</a>
				</li>
				<li class="inline ml-12 text-white">
					<a href="contact" class="hover:border-b-2 hover:animate-[fade_0.1s_ease-in-out]">Contact</a>
				</li>
			</ul>
		</div>
	</div>
</nav>

