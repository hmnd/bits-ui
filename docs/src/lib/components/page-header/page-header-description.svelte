<script lang="ts">
	import type { HTMLAttributes } from "svelte/elements";
	import { cn } from "$lib/utils/styles.js";

	let {
		class: className,
		children,
		...restProps
	}: HTMLAttributes<HTMLParagraphElement> = $props();
</script>

<p
	class={cn(
		"text-foreground/40 mt-3 text-balance text-[21px] font-semibold leading-7 tracking-[-0.01em]",
		className
	)}
	{...restProps}
>
	{@render children?.()}
</p>
