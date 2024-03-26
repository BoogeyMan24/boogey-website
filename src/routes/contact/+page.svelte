<svelte:head>
	<title>Contact | BoogeyMan</title>
</svelte:head>

<script>
	// Thanks to flyte.gg for inspiration/most of the code! Make sure to check them out!
	// 1f0dbc01-4dd1-46c0-aa84-39d66a7ddbc4
	import Nav from "$lib/Nav.svelte";

	let form;

	let emailInput;
	let subjectInput;
	let messageInput;
	let submitButton;

	let email = "";
	let subject = "";
	let message = "";

	let invalidEmail = false;
	let invalidSubject = false;
	let invalidMessage = false;

	let success = "";

	async function submit() {
		invalidEmail = !/^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/.test(email);
		invalidSubject = (subject.length == 0);
        invalidMessage = (message.length == 0);

		let data = {
			"email": email,
			"subject": subject,
			"message": message,
			"accessKey": "1f0dbc01-4dd1-46c0-aa84-39d66a7ddbc4", // Use your own key from https://www.staticforms.xyz 
		};

		if (invalidEmail || invalidSubject || invalidMessage) {
            return false;
        }

		emailInput.disabled = true;
        subjectInput.disabled = true;
        messageInput.disabled = true;
        submitButton.disabled = true;

		form = document.getElementById("form");

		try {
            const res = await fetch('https://api.staticforms.xyz/submit', {
                method: 'POST',
                body: JSON.stringify(data),
                headers: {'Content-Type': 'application/json'}
            });

            const json = await res.json();

            success = json.success ? "true" : "false";
        } catch (e) {
            console.log('[ERROR]', e);
            success = "false";
        }
	}

</script>

<section class="relative overflow-hidden">
	<div class="z-20 relative w-[85%] 2xl:w-[60%] mx-auto h-[12vh]">
		<Nav />
	</div>
</section>
<!-- ABSOLUTE -->
<div class="absolute top-0 bottom-0 overflow-hidden pointer-events-none">
		<img src="s/blue-accent.png" alt="" class="opacity-35">
</div>
<section>
	<!-- Credit to flyte.gg website for inspiration and for some components of the code -->
	<div class="w-[85%] 2xl:w-[60%] mx-auto mt-[8vh]">
		<div class="flex flex-col justify-center">
			<h1 class="text-white text-4xl mb-4">Get in touch</h1>
			<h2 class="text-white text-xl"><span class="opacity-60">Email me at </span><a href="mailto:contact@boogey.dev" target="_blank" class="opacity-80 hover:text-blue-300 transition-all">contact@boogey.dev </a><span class="opacity-60"> or fill out the infomation below.</span></h2>
			
			<div class="flex flex-col gap-12 mt-12">
				<div class="flex flex-wrap md:flex-nowrap gap-8">
					<div class="flex flex-col w-full gap-2">
						<input bind:this={emailInput} bind:value={email} type="email" placeholder="Enter your email address" class="resize-none input">
						{#if invalidEmail}
							<p class="text-[#FF7575] text-md">Invalid email format</p>
						{/if}
					</div>
					<div class="flex flex-col w-full gap-2">
						<input bind:this={subjectInput} bind:value={subject} type="text" placeholder="Enter the subject of the message" class="resize-none input">
						{#if invalidSubject}
							<p class="text-[#FF7575] text-md">Missing subject</p>
						{/if}
					</div>
				</div>
				<div class="flex flex-col w-full gap-2">
					<textarea bind:this={messageInput} bind:value={message} placeholder="Type your message here" class="resize-none input textInput"></textarea>
					{#if invalidMessage}
						<p class="text-[#FF7575] text-md">Missing message</p>
					{/if}
				</div>
			</div>
		</div>
		<div class="flex justify-center items-center flex-col mt-12 mb-16 gap-4">
			<button bind:this={submitButton} on:click={submit} type="submit"class="bg-white h-10 w-36 rounded-md">Submit</button>
			{#if success == "true"}
				<p class="text-[#75FFB3] text-md">Your message has been successfully sent!</p>
			{:else if success == "false"}
				<p class="text-[#FF7575] text-md">There was an error when trying to send your message.</p>
			{/if}
		</div>
	</div>
</section>

<style lang="postcss">
	.input {
		border: 3px solid rgba(100,100,100,0.2);
		border-radius: 8px;
		background-color: #171a1b;
		height: 60px;
		padding-left: 1rem;
		font-size: 1.2rem;
		color: white;
		caret-color: white;
	}

	.textInput {
		padding-top: 1rem;
		height: 250px;
	}
</style>