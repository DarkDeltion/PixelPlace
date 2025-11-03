<template>
  <!-- Single toolbar button. Use the `label` prop for tooltip text or a slot for custom content -->
  <button class="tool-btn" type="button">
    <!-- priority: default slot (custom icon) -> src prop image -> fallback imglabel text -->
    <slot>
      <template v-if="src">
        <img :src="src" alt="" class="tool-icon" />
      </template>
      <template v-else>
        <span class="img">{{ imglabel }}</span>
      </template>
    </slot>

    <span class="tooltip">{{ label }}</span>
  </button>
</template>

<script setup>
const props = defineProps({
  label: { type: String, default: 'Tool' },
  imglabel: { type: String, default: 'Img' },
  src: { type: String, default: '' }
})
</script>

<style scoped>
  /* single button styles (kept from original toolbar button styling) */
  .tool-btn {
    position: relative;
    width: 60px;
    height: 60px;
    border: 1px solid rgba(0,0,0,0.06);
    background: #f2f2f3; /* lighter button background for visibility */
    border-radius: 10px;
    cursor: pointer;
    transition: background 0.15s, transform 0.15s, box-shadow 0.15s;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    box-shadow: 0 1px 2px rgba(0,0,0,0.04);
  }

  .tool-btn:hover {
    background: #e6e7e8;
    transform: translateY(-3px);
    box-shadow: 0 4px 8px rgba(0,0,0,0.08);
  }

  .tooltip {
    position: absolute;
    bottom: -30px;
    left: 50%;
    transform: translateX(-50%) scale(0.9);
    background: #2b2b2b;
    color: #fff;
    padding: 5px 10px;
    border-radius: 6px;
    font-size: 12px;
    white-space: nowrap;
    opacity: 0;
    pointer-events: none;
    transition: opacity 0.2s, transform 0.2s;
  }

  .tool-btn:hover .tooltip {
    opacity: 1;
    transform: translateX(-50%) scale(1);
  }

  /* icon sizing inside the button */
  .tool-icon {
    /* inner image size (icon glyph) */
    width: 20px;
    height: 20px;
    display: block;
    object-fit: contain;
    /* white background so dark icons pop */
    background: #fff;
    padding: 6px; /* creates the white 'badge' around the icon */
    border-radius: 8px;
    box-shadow: 0 1px 3px rgba(0,0,0,0.18);
  }
</style>