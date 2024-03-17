<script>
	import NavItem from "$lib/NavItem.svelte";
</script>

<nav class="pt-10 pb-12">
	<div class="flex justify-between items-center flex-nowrap">
		<logo>
			<a href="/"><img src="/s/misc/pfp.png" alt="pfp logo" class="aspect-square rounded-full w-10 h-auto"></a>
		</logo>
		<div class="">
			<ul class="">
				<!-- <NavItem href="my-journey" name="My Journey" /> -->
				<NavItem href="projects" name="Projects" />
				<NavItem href="about-me" name="About Me" />
				<NavItem href="contact" name="Contact" />
			</ul>
		</div>
	</div>
</nav>

