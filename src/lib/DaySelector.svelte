<script>
  export let schedule;        // timetable schedule object (days as keys)
  export let selectedDay;     // currently selected day
  export let onChange;        // callback to notify parent of changes
</script>

<div id="day-selector">
  <label for="day-select">View Schedule:</label>
  <select
    id="day-select"
    bind:value={selectedDay}
    on:change={(e) => onChange(e.target.value)}
  >
    <option value="full-week">Full Week</option>
    {#each Object.keys(schedule) as day}
      <option value={day}>{day}</option>
    {/each}
  </select>
</div>

<style>
  #day-selector {
    margin-bottom: 1rem;
    text-align: center;
  }

  label {
    margin-right: 0.5rem;
    font-weight: bold;
  }

  select {
    padding: 0.5rem;
    border-radius: 4px;
    border: 1px solid #ccc;
  }
</style>