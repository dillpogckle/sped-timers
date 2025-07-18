<script>
    import { writable } from 'svelte/store';
    import Input from "$lib/Input.svelte";

    let scheduleName = '';
    let timers = writable([{ start:'', hour: '', minute: '', second: '' }]);

    function addTimer() {
        timers.update((list) => [...list, { hour: '', minute: '', second: '' }]);
    }

    function removeTimer(index) {
        timers.update((list) => list.filter((_, i) => i !== index));
    }
</script>

<h1>Create Timer Schedule</h1>

<label>
    Schedule Name:
    <input bind:value={scheduleName} />
</label>

{#each $timers as timer, index}
    <div>2
        <label>
            Start Time:
            <input type="time" bind:value={timer.start}>
        </label>
        <label>
            Hour:
            <input type="number" bind:value={timer.hour} min="0" max="23" />
        </label>
        <label>
            Minute:
            <input type="number" bind:value={timer.minute} min="0" max="59" />
        </label>
        <label>
            Second:
            <input type="number" bind:value={timer.second} min="0" max="59" />
        </label>
        <button type="button" on:click={() => removeTimer(index)}>Remove</button>
    </div>
{/each}

<button type="button" on:click={addTimer}>Add Timer</button>
