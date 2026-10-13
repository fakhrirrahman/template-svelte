<script lang="ts">
	import { useSidebar } from '#lib/components/ui/sidebar/index.js';
	import { Moon, Sun, Bell, Menu } from '@lucide/svelte';

	import { onMount } from 'svelte';

	const sidebar = useSidebar();

	let isDark = $state(false);

	onMount(() => {
		isDark = document.documentElement.classList.contains('dark');
	});

	function toggleTheme() {
		isDark = !isDark;
		if (isDark) {
			document.documentElement.classList.add('dark');
		} else {
			document.documentElement.classList.remove('dark');
		}
	}
</script>

<header class="sticky top-0 z-20 flex h-14 shrink-0 items-center border-b bg-background/80 backdrop-blur-sm">
	<div class="flex w-full items-center gap-3 px-4">
		<!-- Menu button — visible only when sidebar is collapsed -->
		<button
			onclick={() => sidebar.toggle()}
			class="flex h-9 w-9 items-center justify-center rounded-lg text-muted-foreground
				   hover:bg-muted hover:text-foreground transition-colors duration-200"
			aria-label="Open sidebar"
		>
			<Menu class="size-5" />
		</button>

		<!-- Spacer -->
		<div class="flex-1"></div>

		<!-- Right Actions -->
		<div class="flex items-center gap-1">
			<!-- Theme Toggle -->
			<button
				onclick={toggleTheme}
				class="flex h-9 w-9 items-center justify-center rounded-lg text-muted-foreground
					   hover:bg-muted hover:text-foreground transition-colors duration-200"
				aria-label="Toggle theme"
			>
				{#if isDark}
					<Sun class="size-[18px]" />
				{:else}
					<Moon class="size-[18px]" />
				{/if}
			</button>

			<!-- Notifications -->
			<button
				class="relative flex h-9 w-9 items-center justify-center rounded-lg text-muted-foreground
					   hover:bg-muted hover:text-foreground transition-colors duration-200"
				aria-label="Notifications"
			>
				<Bell class="size-[18px]" />
				<span class="absolute right-1.5 top-1.5 flex h-2 w-2">
					<span class="absolute inline-flex h-full w-full animate-ping rounded-full bg-destructive opacity-75"></span>
					<span class="relative inline-flex h-2 w-2 rounded-full bg-destructive"></span>
				</span>
			</button>

			<!-- User Avatar -->
			<button
				class="ml-2 flex h-8 w-8 items-center justify-center rounded-full
					   bg-secondary text-secondary-foreground text-xs font-semibold
					   hover:ring-2 hover:ring-primary/30 transition-all duration-200"
				aria-label="User menu"
			>
				AM
			</button>
		</div>
	</div>
</header>
