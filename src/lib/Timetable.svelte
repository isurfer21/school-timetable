<script>
  import { onMount } from "svelte";
  import { parse } from "yaml";

  import DaySelector from "./DaySelector.svelte";
  import PeriodCell from "./PeriodCell.svelte";

  let timeTableData = null;
  const periodKeys = [
    "Yoga",
    "Assembly",
    "P1",
    "P2",
    "P3",
    "LUNCH",
    "P4",
    "P5",
  ];

  let selectedDay = "full-week";
  let rows = [];

  onMount(async () => {
    try {
      const res = await fetch("./timetable.yaml");
      // if (!res.ok) throw new Error(`Response status: ${res.status}`);

      const data = await res.text();
      console.log("Fetched YAML:", data);

      // Parse YAML from the "content" property
      timeTableData = parse(data);

      // Set default day
      const currentDay = new Date()
        .toLocaleDateString("en-US", { weekday: "long" })
        .toUpperCase();

      if (timeTableData.schedule?.[currentDay]) {
        selectedDay = currentDay;
      }
    } catch (err) {
      console.error("Failed to fetch timetable:", err);
    }
  });

  // Reactive update when selectedDay changes
  $: if (timeTableData) {
    rows =
      selectedDay === "full-week"
        ? Object.keys(timeTableData.schedule)
        : [selectedDay];
  }
</script>

<div class="container">
  {#if timeTableData}
    <h1 class="text-2xl mb-5">
      <img src="./logo.png" alt={timeTableData.class_name} class="logo" />
      {timeTableData.class_name} Time Table
    </h1>

    <DaySelector
      schedule={timeTableData.schedule}
      bind:selectedDay
      onChange={(val) => (selectedDay = val)}
    />

    <table id="timetable">
      <thead>
        <tr>
          <th style="width: 10%;">TIME / DAY</th>
          {#each Object.entries(timeTableData.time_slots) as [key, slot]}
            <th>{slot}<br />({key})</th>
          {/each}
        </tr>
      </thead>
      <tbody>
        {#each rows as day}
          <tr>
            <td class="day-header">{day}</td>
            {#each periodKeys as key}
              <PeriodCell
                periodKey={key}
                periodData={timeTableData.schedule[day][key]}
              />
            {/each}
          </tr>
        {/each}
      </tbody>
    </table>
  {:else}
    <p>Loading timetable...</p>
  {/if}
</div>

<style>
  .container {
    max-width: 1000px;
    margin: auto;
    background: white;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  }
  h1 {
    color: #5a2c85;
    text-align: center;
  }
  .day-header {
    background-color: #7d549c !important;
    color: white;
    font-weight: bold;
  }
  .logo {
    height: 48px;
    vertical-align: middle;
    margin-right: 10px;
  }
</style>
