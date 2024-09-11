<script>
	import { FetchInterceptorV2 } from '@stratech-team/svelte-component-library';

	//Import all the styling for the app
	import '../app.css';
	// data returned from the +layout.js (ENV data)
	export let data;
</script>

<FetchInterceptorV2 {data} />

<slot />
