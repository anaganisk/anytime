<script>
	import moment from "moment-timezone";
	import { onMount } from 'svelte';
    let timenow = moment().format("HH:mm:ss");
    let datenow = moment().format("DD, MMM YYYY")
    const timezones = moment.tz.names();
    
    $: timezone = moment.tz.guess();

	function changeTimeZone(){
        moment.tz.setDefault(timezone);
	}

	onMount(() => {
		const interval = setInterval(() => {
            timenow = moment().format("hh:mm:ss A");
            datenow = moment().format("DD, MMM YYYY");
		}, 1000);

		return () => {
			clearInterval(interval);
		};
	});
</script>

<main>
	<h1 class="time-now">{ timenow }</h1>
    <h5 class="date-now">{ datenow }</h5>
    <form>
	    <label for="timezone">Change Timezone (for current time):</label>
		<select name="timezone" bind:value={timezone} on:change={changeTimeZone}>
            {#each timezones as tz}
                <option value={tz}>{tz}</option>
            {/each}
        </select>
	</form>
</main>

<style>
    main {
		display: flex;
		flex-direction: column;
        align-items: flex-start;
        margin: 2vh 1vw;
    }
	.time-now {
        color: #272038;
        margin: 1px 0px;
		text-transform: uppercase;
		font-size: 4rem;
		font-weight: 700;
    }
    .date-now {
        color: #272038;
        margin: 1px 0px;
		text-transform: uppercase;
		font-size: 1.3rem;
		font-weight: 700;
    }
    select, form {
        width: 100%;
    }

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>