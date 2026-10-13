<script lang="ts">
	import { SidebarProvider, SidebarInset } from '#lib/components/ui/sidebar/index.js';
	import AppSidebar from '#lib/components/layout/AppSidebar.svelte';
	import Navbar from '#lib/components/layout/Navbar.svelte';
	import type { Snippet } from 'svelte';

	let { children }: { children: Snippet } = $props();
</script>

<SidebarProvider>
	<AppSidebar />
	<SidebarInset class="overflow-hidden">
		<Navbar />
		<div class="flex-1 overflow-auto p-6">
			{@render children()}
		</div>
	</SidebarInset>
</SidebarProvider>