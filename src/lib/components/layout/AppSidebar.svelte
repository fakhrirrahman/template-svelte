<script lang="ts">
	import {
		Sidebar,
		SidebarContent,
		SidebarFooter,
		SidebarGroup,
		SidebarGroupContent,
		SidebarGroupLabel,
		SidebarHeader,
		SidebarMenu,
		SidebarMenuButton,
		SidebarMenuItem,
		SidebarSeparator,
	} from '#lib/components/ui/sidebar/index.js';
	import {
		LayoutDashboard,
		Signal,
		Network,
		Shield,
		Server,
		FileText,
		FileSpreadsheet,
		Database,
	} from '@lucide/svelte';
	import { page } from '$app/state';
	import type { Component } from 'svelte';

	type NavItem = {
		title: string;
		url: string;
		icon: Component<{ class?: string }>;
	};

	type NavGroup = {
		label: string;
		items: NavItem[];
	};

	const navGroups: NavGroup[] = [
		{
			label: 'Dashboard',
			items: [
				{ title: 'Overview', url: '/dashboard', icon: LayoutDashboard },
			],
		},
		{
			label: 'Operations (Teams)',
			items: [
				{ title: 'L1 NSOC', url: '/teams/l1-nsoc', icon: Signal },
				{ title: 'L2 NOC', url: '/teams/l2-noc', icon: Network },
				{ title: 'L2 SOC', url: '/teams/l2-soc', icon: Shield },
				{ title: 'L2 MENE', url: '/teams/l2-mene', icon: Server },
			],
		},
		{
			label: 'Reports & Data',
			items: [
				{ title: 'Reports', url: '/reports', icon: FileText },
				{ title: 'Summary Q1 2026', url: '/summary', icon: FileSpreadsheet },
				{ title: 'Excel Data', url: '/data', icon: Database },
			],
		},
	];

	function isActive(itemUrl: string): boolean {
		return page.url.pathname === itemUrl || page.url.pathname.startsWith(itemUrl + '/');
	}
</script>

<Sidebar collapsible="icon">
  <!-- ─── Branding Header ─── -->
  <SidebarHeader class="p-4 group-data-[collapsible=icon]:p-2 group-data-[collapsible=icon]:flex group-data-[collapsible=icon]:justify-center">
    <a
      href="/dashboard"
      class="flex items-center gap-3 group-data-[collapsible=icon]:justify-center group-data-[collapsible=icon]:size-8"
    >
      <div
        class="flex size-8 shrink-0 items-center justify-center rounded-lg bg-primary text-primary-foreground font-bold text-sm shadow-sm shadow-primary/20"
      >
        N
      </div>
      <div class="flex flex-col min-w-0 group-data-[collapsible=icon]:hidden">
        <span
          class="text-sm font-semibold leading-tight tracking-tight text-sidebar-foreground truncate"
          >NSOC KPI</span
        >
        <span
          class="text-[10px] font-medium uppercase tracking-widest text-muted-foreground truncate"
        >
          Executive Suite
        </span>
      </div>
    </a>
  </SidebarHeader>

  <SidebarSeparator />

  <!-- ─── Navigation Groups ─── -->
  <SidebarContent class="px-2 py-2">
    {#each navGroups as group}
      <SidebarGroup>
        <SidebarGroupLabel
          class="text-[10px] font-semibold uppercase tracking-wider text-muted-foreground px-3 mb-1"
        >
          {group.label}
        </SidebarGroupLabel>
        <SidebarGroupContent>
          <SidebarMenu>
            {#each group.items as item}
              <SidebarMenuItem>
                <SidebarMenuButton
                  isActive={isActive(item.url)}
                  tooltipContent={item.title}
                  class={isActive(item.url)
                    ? "bg-primary/15 text-primary font-medium hover:bg-primary/20 hover:text-primary"
                    : ""}
                >
                  {#snippet child({ props })}
                    <a href={item.url} {...props}>
                      <item.icon class="size-4" />
                      <span>{item.title}</span>
                    </a>
                  {/snippet}
                </SidebarMenuButton>
              </SidebarMenuItem>
            {/each}
          </SidebarMenu>
        </SidebarGroupContent>
      </SidebarGroup>
    {/each}
  </SidebarContent>

  <!-- ─── Footer with User Avatar ─── -->
  <SidebarFooter class="p-4 group-data-[collapsible=icon]:p-2 group-data-[collapsible=icon]:flex group-data-[collapsible=icon]:justify-center">
    <div
      class="flex items-center gap-3 group-data-[collapsible=icon]:justify-center group-data-[collapsible=icon]:size-8"
    >
      <div
        class="flex size-8 shrink-0 items-center justify-center rounded-full bg-primary text-primary-foreground text-xs font-semibold"
      >
        N
      </div>
      <div class="flex flex-col min-w-0 group-data-[collapsible=icon]:hidden">
        <span class="text-xs font-medium text-sidebar-foreground truncate">NSOC Admin</span>
        <span class="text-[10px] text-muted-foreground truncate">admin@nsoc.id</span>
      </div>
    </div>
  </SidebarFooter>
</Sidebar>
