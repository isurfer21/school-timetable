<script>
  export let periodKey;
  export let periodData;

  // Function to extract last part of the link for display (if needed)
  function getMeetingId(link) {
    try {
      const url = new URL(link);
      return url.pathname.split("/").filter(Boolean).pop() || link;
    } catch {
      return link;
    }
  }
</script>

{#if periodKey === "LUNCH"}
  <td class="lunch-break">
    {periodData.subject}
  </td>
{:else if periodData.meet_link}
  <!-- Entire cell is clickable -->
  <td
    class="period clickable"
    on:click={() => window.open(periodData.meet_link, "_blank")}
    title="Click to join meeting → {getMeetingId(periodData.meet_link)}"
  >
    <div class="cell-content">
      <p><strong>{periodData.subject}</strong></p>

      {#if periodData.teacher}
        <p>{periodData.teacher}</p>
        {#if periodData.classroom_code}
          <p class="meet-code">{periodData.classroom_code}</p>
        {/if}
      {/if}
    </div>
  </td>
{:else}
  <!-- Non-clickable cell (no meet link) -->
  <td class="period">
    <div class="cell-content">
      <p><strong>{periodData.subject}</strong></p>

      {#if periodData.teacher}
        <p>{periodData.teacher}</p>
        {#if periodData.classroom_code}
          <p class="meet-code">{periodData.classroom_code}</p>
        {/if}
      {/if}
    </div>
  </td>
{/if}

<style>
  td.period {
    vertical-align: top;
    padding: 8px;
    transition: background-color 0.2s ease;
  }

  .clickable {
    cursor: pointer;
  }

  .clickable:hover {
    background-color: honeydew; /* light highlight */
  }

  .cell-content {
    display: flex;
    flex-direction: column;
    height: 100%;
  }

  .meet-code {
    color: yellow;
    background-color: goldenrod;
    padding: 2px 5px;
    border-radius: 15px;
    margin-top: 1px;
  }

  .lunch-break {
    background-color: #fcebeb;
    color: #cc3333;
    font-weight: bold;
  }
</style>
