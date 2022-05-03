<script>
  import { getContext } from "svelte";

  import MonthTitle from "./MonthTitle.svelte";
  import Prev from "./Prev.svelte";
  import Next from "./Next.svelte";
  import FinishBtn from "./FinishBtn.svelte";
  import YearSelector from "./YearSelector.svelte";

  let praecoxCalendarData = getContext("praecoxCalendarData");
</script>

{#if $praecoxCalendarData.yearSelector}
  <div class="divider"></div>
  <YearSelector/>
{/if}

<div class="header">
  <MonthTitle />
  <Prev />
  <Next />

  {#if $praecoxCalendarData.finishBtn}
    <FinishBtn />
  {/if}
</div>
<div class="divider"></div>

<style>
  .header {
    display: flex;
    width: var(
      --praecox-calendar-custom-inner-width,
      var(--praecox-calendar-inner-width)
    );
    height: var(
      --praecox-calendar-custom-head-height,
      var(--praecox-calendar-head-height)
    );
  }

  .divider {
    margin: 0 auto;
    height: 1px;
    margin: 8px auto;
    overflow: hidden;
    background-color: #EBF0F5;
  }
</style>
