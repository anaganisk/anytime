<script>
	import moment from "moment-timezone";

    const timezones = moment.tz.names();
    let timezone = moment.tz.guess();
    let format = "iso";
    
    let timestring = moment().tz(timezone).toISOString();
    let formatstring = "YYYY-MM-DDTHH:mm:ss.sssZ"
    $: data = []

	function addTz(event){
        const newTz = event.target.timezone.value;
        if(format == 'iso') {
            const tzData = moment(timestring).tz(timezone).format("DD, MMM YYYY  hh:mm:ss A");
            data.push({
                time: tzData,
                zone: newTz
            })
            data = data
        } else {
            const tzData = moment(timestring, formatstring).tz(timezone).format("DD, MMM YYYY  hh:mm:ss A");
            data.push({
                time: tzData,
                zone: newTz
            })
            data = data
        }
	}

    function changeString(e) {
        timestring = e.target.value;
        data = []
    }
    

</script>

<main>
	<div>
        <fieldset>
            <legend>Convert Zone: Edit the fields</legend>
            <label for="timestamp">Timestamp:</label>
            <input type="text" name="timestamp" class="full-width" bind:value={timestring} on:input={changeString}>
            <label for="format">Timestamp format:</label>
            <select name="format" bind:value={format}>
                <option value="iso">ISO8601 or RFC2822</option>
                <option value="custom">Custom</option>
            </select>
            {#if format == "custom"}
                <label for="formatstring">Custom format ( <a target="_blank" href="https://momentjs.com/docs/#/displaying/format/">Refer Moment.js formats</a> ):</label>
                <input type="text" name ="formatstring" class="full-width" bind:value={formatstring}>
            {/if}
            <label for="timezone">Add Timezone:</label>
            <form class="button-input" on:submit|preventDefault="{addTz}">
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
    .full-width {
        width: 95%;
    }
    select, form {
            width: 100%;
        }
    .button-input {
        display: flex;
    }
    .data li {
        font-size: 20px;
    }

</style>