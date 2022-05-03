<script>
  import { getContext, onMount } from "svelte";

  let praecoxCalendar = getContext("praecoxCalendarData");

  let yearList = [];
  const showYearTotal = 5;
  let temporarilyArray = [];

  let ty = new Date($praecoxCalendar.viewDate).getFullYear();

  onMount(() => {
    let ty = new Date($praecoxCalendar.viewDate).getFullYear();
    for (let index = 0; index < showYearTotal; index++) {
      yearList[index] = ty + (-1 * ((showYearTotal - 1) / 2) + index);
    }
  });

  function pickYear(i) {
    let d = new Date($praecoxCalendar.viewDate);
    let tm = d.getMonth() + 1;
    let td = d.getDate();
    $praecoxCalendar.viewDate = `${i}-${tm}-${td}`;
  }

  $: ty = new Date($praecoxCalendar.viewDate).getFullYear();
  $: for (let index = 0; index < showYearTotal; index++) {
      yearList[index] = ty + (-1 * ((showYearTotal - 1) / 2) + index);
    };


</script>

<div class="year-spinner">
  <table>
    <tr role="row">
      {#each yearList as item, _i}
        <td role="gridcell" on:click={() => pickYear(item)}>
          <span
            role="presentation"
            class=" praecox-Calendar-month"
            class:current-year={new Date(
              $praecoxCalendar.viewDate
            ).getFullYear() === item}
          >
            {item}
          </span>
        </td>
      {/each}
    </tr>
  </table>
</div>

<style>
  .year-spinner {
    margin: 4px auto;
    width: var(
      --praecox-calendar-custom-inner-width,
      var(--praecox-calendar-inner-width)
    );
    height: var(
      --praecox-calendar-custom-head-height,
      var(--praecox-calendar-head-height)
    );
    color: #A4A8B0;
  }

  tr {
    display: inline-flex;
    justify-content: flex-start;
    border-bottom: 0.5px solid;
    border-color: #EBF0F5;
  }
  td,
  .praecox-Calendar-month {
    display: inline-flex;
    justify-content: center;
    line-height: var(
      --praecox-calendar-custom-head-height,
      var(--praecox-calendar-head-height)
    );
    height: var(
      --praecox-calendar-custom-head-height,
      var(--praecox-calendar-head-height)
    );
    width: calc(var(--praecox-calendar-inner-width) / 5);
    color: #A4A8B0;
    font-family: var(
      --praecox-calendar-custom-number-font-family,
      var(--praecox-calendar-number-font-family)
    );
  }
  .praecox-Calendar-month:hover {
    cursor: pointer;
    background: var(
      --praecox-calendar-custom-background-hover,
      var(--praecox-calendar-background-hover)
    );
  }
  .current-year {
    color: var(
      --praecox-calendar-custom-font-main-color,
      var(--praecox-calendar-font-main-color)
    );
    border-bottom: 0.5px solid;
    border-color: var(
      --praecox-calendar-custom-font-main-color,
      var(--praecox-calendar-font-main-color)
    );
  }
</style>
