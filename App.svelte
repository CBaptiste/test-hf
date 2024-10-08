<script>
  import RadialProgress from "./RadialProgress.svelte";
  let radials = [
    {
      title: "battery",
      format: "%",
      tooltip: "this means XXXX",
      size: 20,
      max: 100,
      colors: [
        { color: "#FF4C4C", from: 0 },
        { color: "#FF944C", from: 25 },
        { color: "#FFC14C", from: 50 },
        { color: "#B4E64C", from: 75 },
        { color: "#4CAF50", from: 100 },
      ],
    },
    {
      title: "CPU",
      format: "M",
      size: 40,
      tooltip: "this means YYYY",
      max: 100,
      colors: [
        { color: "#FF4C4C", from: 0 },
        { color: "#FFC14C", from: 25 },
        { color: "#FF944C", from: 50 },
        { color: "#B4E64C", from: 75 },
        { color: "#4CAF50", from: 100 },
      ],
    },
    {
      title: "Memory",
      format: "Gb",
      size: 120,
      tooltip: "this means ZZZZ",
      max: 190,
      colors: [
        { color: "#FF4C4C", from: 0 },
        { color: "#FF944C", from: 25 },
        { color: "#FFC14C", from: 50 },
        { color: "#B4E64C", from: 75 },
        { color: "#4CAF50", from: 100 },
      ],
    },
    {
      title: "Signups",
      format: "Nb",
      size: 120,
      max: 140,
      tooltip: "this means KKKK",
      colors: [
        { color: "#FF4C4C", from: 0 },
        { color: "#FF944C", from: 25 },
        { color: "#FFC14C", from: 50 },
        { color: "#B4E64C", from: 75 },
        { color: "#4CAF50", from: 100 },
      ],
    },
    {
      title: "Target",
      format: "$",
      size: 140,
      max: 140,
      tooltip: "this means KKKK",
      colors: [
        { color: "#FF4C4C", from: 0 },
        { color: "#FF944C", from: 25 },
        { color: "#FFC14C", from: 50 },
        { color: "#B4E64C", from: 75 },
        { color: "#4CAF50", from: 100 },
      ],
    },
  ];
  let strokeWidth = 10;
  let radius = 20;
</script>

<div class="mt-5 grid gap-y-2">
  <div class="w-full text-sm flex flex-wrap items-center justify-center ">
    <label class="w-1/3 flex flex-wrap items-center justify-right"
      >Diameter
    </label>
    <div class="flex flex-wrap items-center center text-xs gap-x-2">
      <input type="range" min="10" max="40" bind:value={radius} />
      <span
        class="w-12 text-center justify-center inline-flex items-center rounded-md bg-indigo-50 px-2 py-1 text-xs font-medium text-indigo-700 ring-1 ring-inset ring-indigo-700/10"
        >{radius}px</span
      >
    </div>
  </div>

  <div class="w-full text-sm flex flex-wrap items-center justify-center gap-x-">
    <label class="w-1/3 flex flex-wrap items-center justify-right"
      >Stroke Width</label
    >
    <div class="flex flex-wrap items-center center text-xs gap-x-2">
      <input type="range" min="1" max="20" bind:value={strokeWidth} />
      <span
        class="w-12 text-center justify-center inline-flex items-center rounded-md bg-indigo-50 px-2 py-1 text-xs font-medium text-indigo-700 ring-1 ring-inset ring-indigo-700/10"
        >{strokeWidth}px</span
      >
    </div>
  </div>
  <div class="w-full pt-8 flex flex-wrap items-center justify-center">
    <RadialProgress {radials} {strokeWidth} {radius} />
  </div>
</div>
