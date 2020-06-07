<script>
	import moment from "moment-timezone";
    
    $: timestring = moment().toISOString();
    let formatstring = "YYYY-MM-DDTHH:mm:ss.sssZ"

	function getEpoch(data) {
        const d = moment(data).valueOf();
        return d ? d : "";
    }
    

</script>

<main>
	<div>
        <fieldset>
            <legend>Date Time to Epoch(ISO8601 or RFC2822): Edit the fields</legend>
            <label for="timestamp">Timestamp:</label>
            <input type="text" name="timestamp" class="full-width" bind:value={timestring}>
            <p class="data"><b>{getEpoch(timestring)}</b></p>
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
    .data {
        font-size: 20px;
    }

</style>