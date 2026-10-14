<script lang="ts">
	import { useSidebar } from '#lib/components/ui/sidebar/index.js';
	import { Moon, Sun, Bell, PanelLeftClose, PanelLeftOpen } from '@lucide/svelte';
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
		<!-- Single Sidebar Toggle Button -->
		<button
			onclick={() => sidebar.toggle()}
			class="flex h-8.5 w-8.5 items-center justify-center rounded-lg border border-border/60 bg-background/60 text-muted-foreground
				   hover:bg-muted hover:text-foreground hover:border-border transition-all duration-200 shadow-2xs active:scale-95 cursor-pointer"
			aria-label={sidebar.open ? "Tutup sidebar" : "Buka sidebar"}
			title={sidebar.open ? "Tutup Sidebar (Ctrl+B)" : "Buka Sidebar (Ctrl+B)"}
		>
			{#if sidebar.open}
				<PanelLeftClose class="size-[18px]" />
			{:else}
				<PanelLeftOpen class="size-[18px]" />
			{/if}
		</button>

		<!-- Subtle Separator -->
		<div class="h-4 w-px bg-border/60 mx-1 hidden sm:block"></div>

		<!-- Breadcrumb & Status Context -->
		<div class="hidden sm:flex items-center gap-2 text-xs md:text-sm">
			<span class="text-muted-foreground font-medium">Dashboard</span>
			<span class="text-muted-foreground/40 text-xs">/</span>
			<span class="font-semibold text-foreground tracking-tight">Overview</span>
			<span class="ml-2 inline-flex items-center gap-1.5 rounded-full bg-primary/10 border border-primary/20 px-2 py-0.5 text-[10px] font-semibold text-primary">
				<span class="size-1.5 rounded-full bg-primary animate-pulse"></span>
				Live System
			</span>
		</div>

		<!-- Spacer -->
		<div class="flex-1"></div>

		<!-- Right Actions -->
		<div class="flex items-center gap-1.5">
			<!-- Theme Toggle -->
			<button
				onclick={toggleTheme}
				class="flex h-8.5 w-8.5 items-center justify-center rounded-lg text-muted-foreground border border-transparent
					   hover:border-border/50 hover:bg-muted hover:text-foreground transition-all duration-200 cursor-pointer"
				aria-label="Toggle theme"
				title={isDark ? "Switch to Light Mode" : "Switch to Dark Mode"}
			>
				{#if isDark}
					<Sun class="size-[18px]" />
				{:else}
					<Moon class="size-[18px]" />
				{/if}
			</button>

			<!-- Notifications -->
			<button
				class="relative flex h-8.5 w-8.5 items-center justify-center rounded-lg text-muted-foreground border border-transparent
					   hover:border-border/50 hover:bg-muted hover:text-foreground transition-all duration-200 cursor-pointer"
				aria-label="Notifications"
				title="Notifications"
			>
				<Bell class="size-[18px]" />
				<span class="absolute right-1.5 top-1.5 flex h-2 w-2">
					<span class="absolute inline-flex h-full w-full animate-ping rounded-full bg-destructive opacity-75"></span>
					<span class="relative inline-flex h-2 w-2 rounded-full bg-destructive"></span>
				</span>
			</button>

			<!-- User Avatar -->
			<button
				class="ml-1.5 flex h-8 w-8 items-center justify-center rounded-full
					   bg-secondary text-secondary-foreground text-xs font-semibold
					   hover:ring-2 hover:ring-primary/40 transition-all duration-200 cursor-pointer shadow-2xs"
				aria-label="User menu"
			>
				AM
			</button>
		</div>
	</div>
</header>
