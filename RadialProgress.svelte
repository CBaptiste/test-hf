<script>
  export let radials = [];
  export let strokeWidth = 6;
  export let radius = 60;

  radius = Math.min(Math.max(radius, 10), 30);
  strokeWidth = Math.min(Math.max(strokeWidth, 5), 30);

  $: normalizedRadius = radius + strokeWidth * 2;
  $: circumference = normalizedRadius * 2 * Math.PI;
  $: isSmallLayout = radius < 25;
  $: activeRadialTooltip = undefined;
  $: tooltipX = 0;
  $: tooltipY = 0;

  function getColorForProgress(progress, colors) {
    if (progress < 0) {
      return "#808080";
    }
    let selectedColor = colors[0].color;
    for (let i = colors.length - 1; i >= 0; i--) {
      if (progress >= colors[i].from) {
        selectedColor = colors[i].color;
        break;
      }
    }
    return selectedColor;
  }

  function handleMouseOver(event, index) {
    activeRadialTooltip = index;
    updateTooltipPosition(event);
  }

  function handleMouseMove(event, index) {
    activeRadialTooltip = index;
    updateTooltipPosition(event);
  }

  function handleMouseOut() {
    activeRadialTooltip = undefined;
  }

  function updateTooltipPosition(event) {
    tooltipX = event.clientX + 10;
    tooltipY = event.clientY + 10;
  }
</script>

<div class="grid grid-cols-5">
  {#each radials as model, index}
    <div
      class="w-full cursor-pointer inline-flex items-center justify-center relative"
      style={isSmallLayout ? "height: 230px;" : ""}
      on:mouseover={(e) => {
        handleMouseOver(e, index);
      }}
      on:mouseout={(e) => {
        handleMouseOut();
      }}
      on:mousemove={(e) => {
        handleMouseMove(e, index);
      }}
    >
      <svg height="200" width="200">
        <circle
          class="progress-circle"
          stroke="#e6e6e6"
          fill="transparent"
          stroke-width={strokeWidth}
          r={normalizedRadius}
          cx="100"
          cy="100"
        />
        <circle
          class="progress-circle hover:cursor-pointer"
          stroke={getColorForProgress(
            (model.size / model.max) * 100,
            model.colors
          )}
          fill="transparent"
          stroke-width={strokeWidth}
          stroke-dasharray="{circumference} {circumference}"
          stroke-dashoffset={circumference -
            (model.size > model.max ? 1 : model.size / model.max) *
              circumference}
          r={normalizedRadius}
          cx="100"
          cy="100"
        />
      </svg>

      <div
        class="absolute text-center font-light {isSmallLayout ? 'top-0' : ''}"
      >
        <span class="font-medium block capitalize"
          >{model.title}</span
        >
        <span class="text-xs text-gray-500">{model.size}/{model.max} {model.format}</span>
      </div>
      {#if activeRadialTooltip === index}
        <div
          class="fixed z-50 p-2 text-white rounded text-xxs shadow"
          style="background-color: {getColorForProgress(
            (model.size / model.max) * 100,
            model.colors
          )}; top: {tooltipY}px; left: {tooltipX}px;"
        >
          {radials[index].tooltip}
        </div>
      {/if}
    </div>
  {/each}
</div>

<style>
  .text-xs {
    font-size: 14px;
  }
  .text-xxs {
    font-size: 11px;
  }
  .progress-circle {
    transform: rotate(-90deg);
    transition: stroke-dashoffset 0.35s;
    transform-origin: 50% 50%;
  }
</style>
