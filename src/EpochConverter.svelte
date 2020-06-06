<script>
	import moment from "moment-timezone";

    const timezones = moment.tz.names();

    let epoch = moment().valueOf();
    let timezone = moment.tz.guess();
    $: data = []

	function addTz(event){
        const newTz = event.target.timezone.value;
        const tzData = moment.utc(epoch).tz(newTz).format("DD, MMM YYYY  hh:mm:ss A");
        data.push({
            time: tzData,
            zone: newTz
        })
        data = data
	}
	function refreshEpoch(){
        epoch = moment().valueOf();
        data = []
    }
    function changeEpoch(e) {
        epoch = e.target.value;
        data = []
    }
    

</script>

<main>
	<div>
        <fieldset>
            <legend>Epoch to Zone: Edit the fields</legend>
            <label for="epoch">Epoch Milliseconds:</label>
            <div class="epoch-input">
                <input type="text" name="epoch" bind:value={epoch} on:input={changeEpoch}><br><br>
                <button on:click={refreshEpoch}>Refresh Epoch</button>
            </div>
            <label for="timezone">Add Timezone:</label>
            <form class="epoch-input" on:submit|preventDefault="{addTz}">
                <select name="timezone" bind:value={timezone}>
                    {#each timezones as tz}
                        <option value={tz}>{tz}</option>
                    {/each}
                </select>
                <input type="submit" value="Add" />
            </form>
            <span>You can add multiple timezones to compare.</span>
            <div class="data">
                <ul>
                    {#each data as d}
                        <li>
                            <b>{d.zone}</b> <br />
                            {d.time}
                        </li>
                    {/each}
                </ul>
            </div>
        </fieldset>
    </div>
</main>

<style>
    main {
        margin: 2vh 1vw;
    }
    select, form {
            width: 100%;
        }
    .epoch-input {
        display: flex;
    }
    .data li {
        font-size: 20px;
    }

</style>