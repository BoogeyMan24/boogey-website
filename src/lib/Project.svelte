<script>
	export let src = "/s/projects/printerzam.png";
	export let title = "Title...";
	export let subtitle = "";
	export let description = "Description...";
	export let alt = "Alt";
	export let id = "";
	export let link = "/";

	let mouse = { x: 0, y: 0 };

	function handleMove(event) {
		const rect =  document.getElementById(id).getBoundingClientRect();

		mouse.x = event.clientX - rect.x;
		mouse.y = event.clientY - rect.y;
	}
</script>

<a href="projects/{link}" on:pointermove={handleMove} style="--mouseX:{mouse.x + "px"};--mouseY:{mouse.y + "px"}" class="group cursor-pointer transition-all duration-200 rounded-xl hover:shadow-[0_0_25px_-5px_rgba(0,0,0,0.1)] hover:shadow-[#282c36] hover:scale-[101%] border-[1px] border-gray-800">
	<div class="flex flex-col h-full">
		<div class="peer aspect-video">
			<img {src} {alt} class="w-full h-full bg-cover rounded-t-xl z-50">
		</div>
		<div id="{id}" class="blob relative bg-[#1d2027] h-full rounded-b-xl border-t-[1px] border-gray-800">
			<div class="flex justify-between">
				<div>
					<h1 class="group-hover:text-blue-300 transition-all text-white text-[calc(0..5em_+_0.6vw)] font-bold ml-6 mt-4 inline-block">{@html title}</h1>
					<img src="/s/projects/misc/arrow.svg" alt="" class="opacity-0 group-hover:opacity-100 inline-block transition-all rotate-[135deg] mt-[-0.25rem]">
				</div>
				<h1 class="text-white opacity-70 text-sm font-bold ml-6 mt-[1.2rem] mr-6">{@html subtitle}</h1>
			</div>
			<h1 class="text-white opacity-70 text-sm text-semibold ml-6 mr-6 pt-2 mb-5">{@html description}</h1>
		</div>
	</div>
</a>

<style lang=postcss>
	.blob {
		@apply before:hover:opacity-100 peer-hover:before:opacity-100 before:opacity-0 before:rounded-b-xl before:bg-[radial-gradient(500px_circle_at_var(--mouseX)_var(--mouseY),rgba(255,255,255,0.06),transparent_40%)] before:absolute before:h-full before:top-0 before:left-0 before:w-full before:z-[2];
	}
</style>