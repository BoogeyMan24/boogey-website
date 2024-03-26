<svelte:head>
	<title>Home | BoogeyMan</title>
</svelte:head>

<script>
	// {
	// 	"title": "Spoke SMP",
	// 	"subtitle": "Season 5",
	// 	"description": "A Minecraft SMP for all of Spoke's community!",


	// 	"id": "spokesmp",
	// 	"src": "printerzam",
	// 	"extension": ".png",
	// 	"link": "spokesmp"
	// },

	import Nav from "$lib/Nav.svelte";
	import Project from "$lib/Project.svelte";
	import SocialLink from "$lib/SocialLink.svelte";
  	import { onMount } from "svelte";
	import projects from "$lib/projects.json";

	let limit = 6;

	let projectPath = "/s/projects/";

	let title;

	let scroll;
	let mouse = { x: 0, y: 0 };
	
	let browser = "none";

	

	onMount(() => {
		var r = document.querySelector(':root');

		if (window.navigator.userAgent.includes("Firefox")) {
			browser = "firefox";
			r.style.setProperty('--opacity', "0.10");
			r.style.setProperty('--transperancy', "50%");
		} else if (window.navigator.userAgent.includes("Chrome")) {
			browser = "chrome";
			r.style.setProperty('--opacity', "0.35");
			r.style.setProperty('--transperancy', "25%");
		} else if (window.navigator.userAgent.includes("safari")) {
			browser = "safari";
			r.style.setProperty('--opacity', "0.35");
			r.style.setProperty('--transperancy', "25%");
		} else {
			browser = "none";
		}

		window.addEventListener("scroll", () => {
			scroll = window.scrollY;

			let multiplier = 0.06;

			title.animate({
				margin: `${Math.min(Math.max(scroll * multiplier, 0), 40) + "rem"} 0 0 0`
			}, { duration: 1000, fill: "forwards"});

			moveBlob({ x: mouse.x, y: mouse.y + scroll });
		});
	});


	function handleMove(event) {
		mouse.x = event.clientX;
		mouse.y = event.clientY;
		moveBlob(mouse);
	}

	function moveBlob(position) {
		blob.animate({
			transform: `translate(${position.x - 600}px, ${position.y - 600}px)`,
		}, { duration: 3000, fill: "forwards" });
	}
	

	const scrollToElement = (selector) => {
		const element = document.getElementById(selector);
		console.log("test");
		if (!element) return;
		
		element.scrollIntoView({
			behavior: "smooth",
		});
	}
</script>

<!-- from: #252d3e | to: #171a1b -->
<section on:pointermove={handleMove} class="relative overflow-hidden">
	<div id="blob" class="blob z-0"></div>
	<div class="z-20 relative w-[85%] 2xl:w-[60%] mx-auto h-24">
		<Nav />
	</div>
	<div class="w-[85%] 2xl:w-[60%] mx-auto h-[70lvh] flex flex-col justify-evenly items-center z-20 relative">
		<div bind:this={title} class="z-20 relative transition-all ease-linear">
			<div class="">
				<h1 class="text-white text-7xl font-bold text-center tracking-wide mb-4">Hey, I'm <span class="underline">Boogey</span>!</h1>
				<h2 class="text-gray-300 font-medium text-center mb-4 text-xl">An aspiring software engineer.</h2>
			</div>
			<div class="w-full flex justify-center">
				<button on:click|preventDefault={() => scrollToElement("projects")} class="mt-4 pt-2 pb-2 pl-10 pr-10 rounded-3xl bg-white">My Projects</button>
			</div>
		</div>
		<div></div>
		<!-- ABSOLUTE POSITIONING -->
		<div class="pointer-events-none h-[16rem] md:h-[20rem] xl:h-[24rem] absolute bottom-[-0.1%] w-svw overflow-hidden z-40">
			<img src="s/layered-peaks-haikei.svg" alt="Mountain transition" class="aspect-[960/300] w-full h-full bottom-0 absolute object-left object-cover">
		</div>
	</div>

	
</section>
<section id="projects" on:pointermove={handleMove} class="z-30 relative">
	<div class="z-30 bg-[#121414] pb-28">
		<div class="w-[85%] 2xl:w-[60%] mx-auto">
			<div class="pt-20 pb-12">
				<div class="flex h-[10%] w-full items-center">
					<div class="flex-1">
						<h2 class=" text-white text-4xl"><i>Epic</i> Projects</h2>
						<h2 class="text-gray-400 text-lg mt-2">My Journey (coming soon)</h2>
					</div>
					<SocialLink link="https://github.com/BoogeyMan24" logo="octicons-mark-github"/>
					<div class="ml-4">
						<SocialLink link="https://discordapp.com/users/707265292635734076" logo="discord-mark-white"/>
					</div>
				</div>
			</div>
		</div>
		<div class="w-[85%] 2xl:w-[60%] mx-auto">
			<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 2xl:grid-cols-4 gap-12">
				{#each projects as project, i}
					{#if i < limit}
						<Project id="{project.id}" link="{project.link}" src="{projectPath}{project.src}{project.extension}" title="{project.title}" subtitle="{project.subtitle}" description="{project.description}" />
					{/if}
				{/each}
			</div>
		</div>
	</div>
</section>
<section class="pointer-events-none relative overflow-hidden z-50">
	<div class="pointer-events-none h-[16rem] md:h-[20rem] rotate-180 xl:h-[24rem] bottom-[-0.1%] w-svw overflow-hidden z-40">
		<img src="s/layered-peaks-haikei.svg" alt="Upside down mountain transition" class="aspect-[960/300] w-full h-full bottom-0 absolute object-left object-cover">
	</div>
</section>
<section class="h-96 mt-[-12rem]">
	<div class="w-[85%] h-full 2xl:w-[60%] mx-auto flex justify-center items-center">
		<div class="flex flex-col justify-center items-center">
			<h1 class="test-center text-white text-4xl tracking-wider">Make sure to Check out My Journey! (coming soon!)</h1>
			<button class="mt-12 rounded-3xl bg-white w-56 h-10">Take me there!</button>
		</div>
	</div>
</section>



<style lang="postcss">
	:root {
		--opacity: 0.35;
		--transperancy: 25%;
	}

	.underline {
		content: "";
		width: full;
		background-image: linear-gradient(90deg, rgb(56, 69, 207), rgb(131, 18, 165)); 
		background-size: 100% 6px; 
		background-repeat: no-repeat;
		background-position: left bottom;
		text-decoration: none;
		border-radius: 2px;
	}

	@keyframes rotate {
		from {
			rotate: 0deg;
		}

		50% {
			scale: 1 1.5;
		}

		to {
			rotate: 360deg;
		}
	}

	@keyframes opacity {
		from {
			opacity: 0;
		}

		to {
			opacity: 1;
		}
	}

	.blob {
		opacity: 0;
		z-index: 1;
		position: absolute;
		aspect-ratio: 1;
		border-radius: 50%;
		height: 1200px;
		background: radial-gradient(circle at center,rgba(255,255,255, var(--opacity)),transparent var(--transperancy));
		/* animation: rotate 20s infinite; */
		filter: blur(200px);
		-webkit-filter: blur(200px);
		-moz-filter: blur(200px);

		animation: opacity 1s forwards 1s;
	}
</style>