<script>
	import Clock from "./Clock.svelte";
	import EpochConverter from "./EpochConverter.svelte";
	import TimeZonverter from "./TimeZonverter.svelte";
	import TzToEpoch from "./TzToEpoch.svelte"

	export let name;

	function convert(){

	}

</script>

<main>
	<nav class="nav">
	<a href="/" class="app-title">{name}</a>
	</nav>
	<div class="clock-section">
		<Clock />
	</div>
	<p><b>The timezone defaults to you local system timezone.</b></p>
	<div class="main-section">
		<EpochConverter />
		<TimeZonverter />
		<TzToEpoch />
	</div>
	<footer><a href="https://github.com/anaganisk/anytime">Source on github</a> &copy; 2020 Sai Kiran Anagani</footer>
</main>

<style>
	main {
		width: 95vw;
	}

	.main-section {
		display: flex;
		flex-wrap: wrap;
		align-content: center;
		justify-content: center;
	}
	.clock-section {
		display: flex;
		flex-wrap: wrap;
		align-content: center;
		justify-content: center;
	}
	.nav {
		padding: 20px;
	}
	p{
		text-align: center;
	}

	.app-title {
		color: #2b283b;
		text-transform: uppercase;
		font-size: 2rem;
		font-weight: 700;
		padding: 1vh 1vw;
		border: 8px solid #2b283b;
	}		
</style>