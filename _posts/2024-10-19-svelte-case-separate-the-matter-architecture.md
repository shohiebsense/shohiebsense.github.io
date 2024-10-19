I don't think of a fancy name or whatever, but one of the problem with the JS Projects is a gigantic written code in a single file.  

So separate the matter with any approach you are familiar with, whether it could be ViewModel approach, or just do with you think it feels good.  

I separate the View and Logic, and within the View, I separate the elements and their styles. 

```.md
src/
└── sections/
    └── dashboard/
        ├── DashboardSection.svelte
        ├── DashboardSectionStyles.css
        └── DashboardSectionView.svelte
```


1. **DashboardSection.svelte**
   - This is the main Svelte component for the dashboard section. It handles the logic and rendering of the dashboard content, integrating various sub-components and managing the overall structure of the dashboard section.

2. **DashboardSectionStyles.css**
   - This file contains the custom CSS for styling the `DashboardSection.svelte` component. It includes layout, colors, spacing, and other styling rules to ensure the dashboard section's visual appearance aligns with the overall design of the application.

3. **DashboardSectionView.svelte**
   - This component focuses on the presentation layer of the dashboard. It manages the view logic, separating concerns between UI rendering and business logic, ensuring the modular structure of the dashboard section. This file is designed to be lightweight and focused solely on the visual representation.

So let's say in +page.svelte or your root of a page.

```.svelte
//+page,svelte

<hr class="my-3 border-dark" />
	{#if activeMenu === 'Dashboard'}
		<DashboardSection
			{fetchLogResponse}
			{fetchPendingTransactionResponse}
			{fetchFailedTransactionResponse}
			{lastUpdateDateTime}
			{fetchMrtHeartbeatResponse}
			{fetchLrtHeartbeatResponse}
			{fetchTjHeartbeatResponse}
			{fetchRouteServiceResponse}
			{fetchSuperAppsServiceResponse}
			{triggerUpdateOn}
		/>
		<hr class="my-3 border-dark" />
	{/if}
```

so you do some business logic in there and eventually you just show it like 

```.svelte
//DashboardSection.svelte

<DashboardSectionView
	{superAppErrors}
	{paymentTransactionLogErrors}
	{paymentPendingTransactionErrors}
	{paymentFailedTransactionErrors}
	{mrtDeviceErrors}
	{lrtDeviceErrors}
	{tjDeviceErrors}
	{lastUpdateDateTime}
/>
```

here we go, on `DashboardSectionView.svelte`

```
<script>
	export let superAppErrors;
	export let paymentPendingTransactionErrors;
	export let paymentFailedTransactionErrors;
	export let paymentTransactionLogErrors;
	export let mrtDeviceErrors;
	export let lrtDeviceErrors;
	export let tjDeviceErrors;
	export let lastUpdateDateTime;
</script>

<!-- your component div whatever-->
```


It feels better, more engaging, and encouraging. It's nice
