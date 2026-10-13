<script lang="ts">
	import { CalendarDays, TrendingUp, CheckCircle, AlertTriangle } from '@lucide/svelte';
</script>

<svelte:head>
	<title>Executive KPI Dashboard — NSOC KPI</title>
</svelte:head>

<div class="space-y-6">
	<!-- Page Header -->
	<div class="flex flex-col gap-1 sm:flex-row sm:items-center sm:justify-between">
		<div>
			<h1 class="text-2xl font-semibold tracking-tight">Executive KPI Dashboard</h1>
			<p class="text-sm text-muted-foreground">
				Network Service Operations Center Performance ·
				<span class="text-primary font-medium">Oct 2026</span>
			</p>
		</div>
		<div class="flex items-center gap-2 rounded-lg border bg-card px-3 py-2 text-sm">
			<CalendarDays class="size-4 text-muted-foreground" />
			<span>Oct 01, 2026 – Oct 31, 2026</span>
		</div>
	</div>

	<!-- Top KPI Cards -->
	<div class="grid gap-4 sm:grid-cols-2 lg:grid-cols-3">
		<!-- Total Score -->
		<div class="rounded-xl border bg-card p-5 space-y-2">
			<div class="flex items-center justify-between">
				<span class="text-sm font-medium text-muted-foreground">Total Score</span>
				<span class="text-xs font-medium text-secondary">Oct 2026</span>
			</div>
			<p class="text-3xl font-bold text-primary">95.3%</p>
			<p class="text-xs text-primary font-medium">Same as Sep 2026</p>
		</div>

		<!-- Operational Status -->
		<div class="rounded-xl border bg-card p-5 space-y-2">
			<div class="flex items-center justify-between">
				<span class="text-sm font-medium text-muted-foreground">Operational Status</span>
				<div class="flex items-center gap-1.5 text-primary">
					<CheckCircle class="size-3.5" />
					<span class="text-xs font-medium">Healthy</span>
				</div>
			</div>
			<p class="text-3xl font-bold text-primary">Healthy</p>
			<p class="text-xs text-muted-foreground">Lowest: <span class="font-medium">L2 NOC</span> (90%)</p>
		</div>

		<!-- KPI Achieved -->
		<div class="rounded-xl border bg-card p-5 space-y-2">
			<div class="flex items-center justify-between">
				<span class="text-sm font-medium text-muted-foreground">KPI Achieved</span>
				<span class="text-xs font-medium italic text-muted-foreground">Full Score</span>
			</div>
			<p class="text-3xl font-bold">
				73 <span class="text-muted-foreground font-normal">/ 79</span>
			</p>
			<p class="text-xs text-secondary font-medium">6 KPIs below full score</p>
		</div>
	</div>

	<!-- Team Score Cards -->
	<div class="grid gap-4 sm:grid-cols-2 lg:grid-cols-4">
		{#each [
			{ name: 'L1 NSOC', subtitle: 'NSIM · Level 1', score: 96.8, total: '61 / 63 weight points', color: 'text-primary' },
			{ name: 'L2 NOC', subtitle: 'Network · Level 2', score: 90.0, total: '22.5 / 25 weight points', color: 'text-secondary' },
			{ name: 'L2 SOC', subtitle: 'Security · Level 2', score: 95.0, total: '19 / 20 weight points', color: 'text-primary' },
			{ name: 'L2 MENE', subtitle: 'Maintenance · Level 2', score: 97.5, total: '9.75 / 10 weight points', color: 'text-primary' },
		] as card}
			<div class="rounded-xl border bg-card p-5 flex flex-col items-center text-center space-y-3">
				<div>
					<h3 class="text-sm font-semibold">{card.name}</h3>
					<p class="text-[11px] text-muted-foreground">{card.subtitle}</p>
				</div>

				<!-- Circular Progress Indicator -->
				<div class="relative flex items-center justify-center">
					<svg class="size-24 -rotate-90" viewBox="0 0 100 100">
						<circle
							cx="50" cy="50" r="40"
							fill="none"
							stroke="currentColor"
							stroke-width="8"
							class="text-muted/50"
						/>
						<circle
							cx="50" cy="50" r="40"
							fill="none"
							stroke="currentColor"
							stroke-width="8"
							stroke-linecap="round"
							stroke-dasharray={2 * Math.PI * 40}
							stroke-dashoffset={2 * Math.PI * 40 * (1 - card.score / 100)}
							class={card.color}
						/>
					</svg>
					<span class="absolute text-lg font-bold {card.color}">
						{card.score}<span class="text-xs">%</span>
					</span>
				</div>

				<div>
					<p class="text-xs text-muted-foreground">Overall Score</p>
					<p class="text-[11px] font-medium text-muted-foreground">{card.total}</p>
				</div>
			</div>
		{/each}
	</div>
</div>
