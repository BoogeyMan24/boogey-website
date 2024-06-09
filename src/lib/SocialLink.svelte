<script>
	export let link = "https://www.youtube.com/watch?v=dQw4w9WgXcQ";
	export let logo;
	export let color = "#121414";
</script>


<a href="{link}">
	<div class="aspect-square border-white w-10 h-10">
			<div class="w-full h-full hover:scale-[105%] rounded-lg bg-[{color}] border-[2px] border-[#252931] flex justify-center">
				<img src="/s/misc/{logo}.svg" alt="github logo" class="w-6 h-auto">
			</div>
	</div>
</a>