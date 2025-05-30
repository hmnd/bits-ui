<script lang="ts">
	import { onMount, type Snippet } from "svelte";
	import { Button } from "bits-ui";
	import { scale } from "svelte/transition";
	import { cubicOut } from "svelte/easing";
	import Moon from "phosphor-svelte/lib/Moon";
	import Sun from "phosphor-svelte/lib/Sun";

	let { children }: { children: Snippet } = $props();

	let theme = $state("light");
	let componentName = "%component.name%";

	onMount(() => {
		const systemTheme = window.matchMedia("(prefers-color-scheme: dark)").matches
			? "dark"
			: "light";
		theme = systemTheme;
	});

	function toggleTheme() {
		theme = theme === "light" ? "dark" : "light";
		document.documentElement.setAttribute("class", theme);
	}
</script>

<div class={theme}>
	<div class="bg-background">
		<div class="flex items-center justify-between px-4 py-2">
			{@render Logo()}
			{@render ThemeToggle()}
		</div>

		<main class="flex justify-center p-4">
			<div
				class="border-muted relative flex w-full max-w-3xl items-center justify-center rounded-lg border-2 bg-zinc-50 p-8 shadow-sm dark:bg-neutral-900/50"
			>
				<div
					class="bg-foreground text-background absolute -left-0.5 -top-0.5 select-none rounded-br-md rounded-tl-md px-2 py-1 font-mono text-xs font-medium tracking-tighter"
				>
					{componentName}
				</div>
				{@render children?.()}
			</div>
		</main>
	</div>
</div>

{#snippet ThemeToggle()}
	<Button.Root
		onclick={toggleTheme}
		role="switch"
		aria-label="Light Switch"
		aria-checked={theme === "light"}
		title="Toggle {theme === 'dark' ? 'Dark' : 'Light'} Mode"
		class="rounded-input hover:bg-dark-10 focus-visible:ring-foreground focus-visible:ring-offset-background focus-visible:outline-hidden relative inline-flex h-10 w-10 items-center justify-center px-2 focus-visible:ring-2 focus-visible:ring-offset-2"
	>
		{#if theme === "light"}
			<div
				class="absolute inline-flex h-full w-full items-center justify-center"
				transition:scale={{
					delay: 50,
					duration: 200,
					start: 0.7,
					easing: cubicOut,
				}}
			>
				<Moon class="size-6" aria-label="Moon" />
			</div>
		{:else}
			<div
				class="absolute inline-flex h-full w-full items-center justify-center"
				transition:scale={{
					delay: 50,
					duration: 200,
					start: 0.7,
					easing: cubicOut,
				}}
			>
				<Sun class="size-6" aria-label="Sun" />
			</div>
		{/if}
	</Button.Root>
{/snippet}

{#snippet Logo()}
	<a href="https://bits-ui.com" target="_blank" aria-label="Bits UI">
		<svg
			width="94"
			height="22"
			viewBox="0 0 94 22"
			fill="none"
			xmlns="http://www.w3.org/2000/svg"
		>
			<path
				d="M58.0197 19.3381C55.7317 19.3381 53.8857 18.5581 52.4037 16.9721L54.7697 14.8141C55.7577 15.9321 56.7977 16.4781 57.9417 16.4781C59.1377 16.4781 59.8137 15.8801 59.8137 15.0741C59.8137 14.3721 59.4757 13.9821 57.3437 13.4881C53.7297 12.6301 53.1837 10.9921 53.1837 9.27609C53.1837 6.91009 55.0557 5.14209 58.2277 5.14209C60.4117 5.14209 61.8677 5.68809 63.2457 7.48209L60.6977 9.43209C60.0477 8.39209 59.2157 7.97609 58.3057 7.97609C57.3437 7.97609 56.6157 8.34009 56.6157 9.17209C56.6157 9.64009 56.8237 10.0561 58.4357 10.4721C62.3617 11.4861 63.2717 12.9421 63.2717 14.9701C63.2717 17.4661 61.0097 19.3381 58.0197 19.3381Z"
				fill="currentColor"
			/>
			<path
				d="M49.3294 19C46.6514 19 45.1954 17.752 45.1954 14.814V8.46999H43.2974V5.47999H45.1954V2.74999L48.7054 2.38599V5.47999H51.5654V8.46999H48.7054V14.632C48.7054 15.49 49.1214 15.88 49.7974 15.88H51.2534V19H49.3294Z"
				fill="currentColor"
			/>
			<path
				d="M37.8415 19V5.48003H41.3515V19H37.8415ZM37.4775 2.28203C37.4775 1.16403 38.3875 0.228027 39.5835 0.228027C40.8055 0.228027 41.6895 1.16403 41.6895 2.28203C41.6895 3.45203 40.8055 4.36203 39.5835 4.36203C38.3875 4.36203 37.4775 3.42603 37.4775 2.28203Z"
				fill="currentColor"
			/>
			<path
				d="M28.814 19.338C26.396 19.338 25.174 18.324 24.446 16.79V19H21.04V0.0200195H24.55V7.56002C25.278 6.13002 26.5 5.19402 28.814 5.19402C32.532 5.19402 35.496 8.39202 35.496 12.292C35.496 16.192 32.532 19.338 28.814 19.338ZM24.446 12.292C24.446 14.398 25.928 16.166 28.242 16.166C30.478 16.166 31.986 14.32 31.986 12.266C31.986 10.16 30.478 8.36602 28.242 8.36602C25.928 8.36602 24.446 10.186 24.446 12.292Z"
				fill="currentColor"
			/>
			<circle
				cx="5.93555"
				cy="10.9873"
				r="4.3"
				transform="rotate(90 5.93555 10.9873)"
				fill="currentColor"
			/>
			<g>
				<path
					d="M81,20.4h-7c-2.9,0-5.2-2.4-5.2-5.2v-7c0-2.9,2.4-5.2,5.2-5.2h7c2.9,0,5.2,2.4,5.2,5.2v7C86.2,18,83.9,20.4,81,20.4z M74,4
			c-2.3,0-4.2,1.9-4.2,4.2v7c0,2.3,1.9,4.2,4.2,4.2h7c2.3,0,4.2-1.9,4.2-4.2v-7C85.1,5.8,83.3,4,81,4H74z"
					fill="currentColor"
				/>
			</g>
			<g>
				<path
					d="M77.8,8.1h1.1v4.8c0,0.5-0.1,1-0.4,1.4c-0.2,0.4-0.6,0.7-1,0.9c-0.4,0.2-0.9,0.3-1.5,0.3c-0.6,0-1.1-0.1-1.5-0.3
			c-0.4-0.2-0.8-0.5-1-0.9c-0.2-0.4-0.4-0.8-0.4-1.4V8.1h1.1v4.7c0,0.3,0.1,0.6,0.2,0.9c0.1,0.3,0.4,0.5,0.6,0.6
			c0.3,0.1,0.6,0.2,1,0.2c0.4,0,0.7-0.1,1-0.2c0.3-0.1,0.5-0.4,0.6-0.6c0.1-0.3,0.2-0.6,0.2-0.9V8.1z M81.7,8.1v7.3h-1.1V8.1H81.7z"
					fill="currentColor"
				/>
			</g>
		</svg>
	</a>
{/snippet}
