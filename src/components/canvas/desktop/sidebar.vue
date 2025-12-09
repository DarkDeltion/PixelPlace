<template>
  <div class="sidebar">
    <div class="color-section">
      <div class="color-picker-row">
        <input
          type="color"
          class="color-picker"
          v-model="localColor"
          @input="(e) => emit('update:color', e.target.value)"
          aria-label="Pick brush color"
        />

        <!-- editable hex input: user can type a hex and it will update the color when valid -->
        <input
          class="current-hex-input"
          type="text"
          v-model="hexInput"
          @input="onHexInput"
          @blur="onHexConfirm"
          @keydown.enter.prevent="onHexConfirm"
          aria-label="Edit hex color"
        />
      </div>

      <div class="size-changer">
        <label class="size-label">
          <span>Brush</span>
          <input
            class="size-input"
            type="number"
            v-model.number="size"
            :min="min"
            :max="max"
            :step="step"
            aria-label="Brush size input"
          />
        </label>

        <input
          class="size-range"
          type="range"
          :min="min"
          :max="max"
          :step="step"
          v-model.number="size"
        />
      </div>

      <div class="preset-colors" role="list">
        <button
          v-for="(p, i) in presetColors"
          :key="p + i"
          class="color-swatch"
          :style="{ background: p }"
          @click="selectPreset(p)"
          :aria-label="`Select color ${p}`"
          type="button"
        ></button>
      </div>

      <div class="color-history">
        <div class="history-title">Recent</div>
        <div class="history-grid">
          <button
            v-for="(h, idx) in colorHistory"
            :key="(h || '') + idx"
            class="history-swatch"
            :class="{ placeholder: !h }"
            :style="{ background: h || '#FFFFFF' }"
            @click="selectPreset(h)"
            :aria-label="h ? `Select recent color ${h}` : 'Empty color slot'"
            type="button"
          ></button>
        </div>
      </div>
    </div>
    <router-link to="/" class="home-btn">Home</router-link>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue'

// support v-model from parent: prop is `modelValue`, emit `update:modelValue`

const props = defineProps({
  modelValue: { type: Number, default: 6 },
  // allow parent to customize slider bounds and step
  min: { type: Number, default: 1 },
  max: { type: Number, default: 50 },
  step: { type: Number, default: 1 },
  // support v-model:color
  color: { type: String, default: '#000000' },
})
const emit = defineEmits(['update:modelValue', 'update:color'])

// local numeric size (use number coercion on inputs)
const size = ref(Number(props.modelValue ?? 6))

// local color for the color picker
const localColor = ref(String(props.color ?? '#000000'))

// preset palette and recent history
// preset palette (10 main colors)
const presetColors = [
  '#ff4d4d',
  '#ff8a4d',
  '#ffd24d',
  '#ffee58',
  '#4dff4d',
  '#00bfa5',
  '#4d4dff',
  '#2979ff',
  '#8a4dff',
  '#ff4dd2',
  '#000000',
]

// initialize history with MAX_HISTORY placeholders (null) so selecting white doesn't remove other entries
const MAX_HISTORY = 10
const colorHistory = ref(Array(MAX_HISTORY).fill(null))

// keep local color in sync with parent prop
watch(
  () => props.color,
  (v) => {
    if (typeof v === 'string' && v !== localColor.value) localColor.value = v
  },
)

// hex text input that users can type into
const hexInput = ref(String(localColor.value).toUpperCase())

function normalizeHex(input) {
  if (!input || typeof input !== 'string') return null
  let s = input.trim()
  if (s[0] !== '#') s = '#' + s
  // allow 3 or 6 hex digits
  const three = /^#([0-9a-fA-F])([0-9a-fA-F])([0-9a-fA-F])$/
  const six = /^#([0-9a-fA-F]{6})$/
  const m3 = s.match(three)
  if (m3) {
    // expand #rgb -> #rrggbb
    const r = m3[1]
    const g = m3[2]
    const b = m3[3]
    return ('#' + r + r + g + g + b + b).toUpperCase()
  }
  const m6 = s.match(six)
  if (m6) return s.toUpperCase()
  return null
}

function onHexInput(e) {
  // while typing, only update the local text value. do NOT change the active color.
  // this gives the user full control while typing.
  hexInput.value = e.target.value
}

function onHexConfirm() {
  // user finished editing (Enter or blur). validate and apply; default to black on invalid.
  const normalized = normalizeHex(hexInput.value)
  if (normalized) {
    // apply normalized color (this triggers the localColor watcher which updates history and emits)
    localColor.value = normalized
    // ensure the input shows the normalized form
    hexInput.value = normalized
  } else {
    // invalid -> default to black
    const black = '#000000'
    localColor.value = black
    hexInput.value = black
  }
}

// keep hexInput in sync when localColor changes from other UI (picker, presets)
watch(
  () => localColor.value,
  (v) => {
    if (typeof v === 'string') hexInput.value = String(v).toUpperCase()
  },
)

// emit color changes when localColor changes and update history
watch(localColor, (v) => {
  if (typeof v === 'string') {
    emit('update:color', v)

    try {
      // keep recent colors, newest first, no duplicates, limit MAX_HISTORY
      const hex = v.toUpperCase()
      // remove any existing instance of this color (placeholders are null and won't match)
      colorHistory.value = colorHistory.value.filter((c) => c !== hex)
      // add newest to front
      colorHistory.value.unshift(hex)
      // trim to MAX_HISTORY
      if (colorHistory.value.length > MAX_HISTORY) colorHistory.value.length = MAX_HISTORY
    } catch (e) {
      /* ignore history errors */
    }
  }
})

function selectPreset(hex) {
  if (typeof hex === 'string') localColor.value = hex
}

// keep local size in sync with parent prop
watch(
  () => props.modelValue,
  (v) => {
    const n = Number(v)
    if (!Number.isNaN(n) && n !== size.value) size.value = n
  },
)

// emit numeric changes when the local slider / input changes
watch(size, (v) => {
  const n = Number(v)
  if (!Number.isNaN(n)) emit('update:modelValue', n)
})
</script>

<style scoped>
.sidebar {
  position: fixed;
  right: 0;
  top: 100px; /* below top nav */
  width: 220px;
  height: calc(100vh - 100px);
  background: #1e1e1e;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  padding: 20px;
  box-shadow: -2px 0 10px rgba(0, 0, 0, 0.3);
  z-index: 30; /* sit above the fixed canvas */
}

.color-section {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20px;
}

.color-picker-row {
  display: flex;
  align-items: center;
  gap: 10px;
  width: 100%;
  justify-content: center;
}

.color-picker {
  width: 46px;
  height: 46px;
  border: none;
  padding: 0;
  background: transparent;
  cursor: pointer;
}

.current-color {
  width: 36px;
  height: 36px;
  border-radius: 8px;
  border: 2px solid rgba(255, 255, 255, 0.06);
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.4);
}

.current-hex {
  color: #ddd;
  font-size: 13px;
  font-weight: 600;
  background: rgba(255, 255, 255, 0.02);
  padding: 6px 8px;
  border-radius: 6px;
}

.current-hex-input {
  color: #ddd;
  font-size: 13px;
  font-weight: 600;
  background: rgba(255, 255, 255, 0.02);
  padding: 6px 8px;
  border-radius: 6px;
  border: 1px solid transparent;
  width: 88px;
  text-align: center;
}

.current-hex-input:focus {
  outline: none;
  border-color: rgba(77, 144, 254, 0.4);
  box-shadow: 0 0 0 3px rgba(77, 144, 254, 0.08);
}

.color-wheel {
  width: 150px;
  height: 150px;
  border-radius: 50%;
  background: conic-gradient(red, yellow, lime, cyan, blue, magenta, red);
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.4);
  position: relative;
}

.color-wheel::after {
  content: '';
  position: absolute;
  inset: 20px;
  background: #1e1e1e;
  border-radius: 50%;
}

.preset-colors {
  display: grid;
  grid-template-columns: repeat(6, 1fr);
  gap: 8px;
  width: 100%;
  justify-items: center;
}

.color-swatch {
  width: 40px;
  height: 40px;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  transition: transform 0.2s;
}

.color-swatch:hover {
  transform: scale(1.1);
}

.color-history {
  width: 105%;
  background: #2b2b2b;
  border-radius: 10px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  color: #aaa;
  font-size: 13px;
  padding: 10px;
}

.history-grid {
  margin-top: 6px;
  width: 100%;
  display: grid;
  /* 5 columns so 10 items render as two rows */
  grid-template-columns: repeat(5, 1fr);
  gap: 8px;
  align-items: center;
  justify-items: center;
}

.history-swatch {
  width: 40px;
  height: 40px;
  border: 1px solid rgba(0, 0, 0, 0.12);
  border-radius: 8px;
  padding: 0;
  margin: 0;
}

.history-swatch.placeholder {
  opacity: 0.5;
  box-shadow: inset 0 0 0 1px rgba(0, 0, 0, 0.06);
}

.history-title {
  color: #ddd;
  font-size: 12px;
  font-weight: 700;
  align-self: flex-start;
  margin-left: 6px;
}

.home-btn {
  display: inline-flex; /* allow anchor to take width/height */
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 60px;
  margin-bottom: 20%;
  background: #2b2b2b;
  border: none;
  border-radius: 10px;
  color: #fff;
  font-size: 16px;
  cursor: pointer;
  transition:
    background 0.2s,
    transform 0.2s;
  text-decoration: none;
}

.home-btn:hover {
  background: #3a3a3a;
  transform: translateY(-3px);
}

.size-changer {
  width: 100%;
  display: flex;
  flex-direction: column;
  gap: 8px;
  align-items: center;
}

.size-label {
  width: 100%;
  display: flex;
  justify-content: space-between;
  color: #ddd;
  font-size: 14px;
  padding: 0 6px;
}

.size-value {
  background: rgba(255, 255, 255, 0.06);
  padding: 2px 8px;
  border-radius: 6px;
  color: #fff;
  font-weight: 600;
}

.size-range {
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
  width: calc(100% - 12px);
  height: 8px;
  border-radius: 6px;
  background: linear-gradient(90deg, #4d90fe, #8e44ad);
  outline: none;
}

.size-range::-webkit-slider-thumb {
  -webkit-appearance: none;
  width: 18px;
  height: 18px;
  border-radius: 50%;
  background: #fff;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.3);
  cursor: pointer;
}

.size-range::-moz-range-thumb {
  width: 18px;
  height: 18px;
  border-radius: 50%;
  background: #fff;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.3);
  cursor: pointer;
}

.size-input {
  background: rgba(255, 255, 255, 0.04);
  border: 1px solid rgba(255, 255, 255, 0.06);
  color: #fff;
  padding: 2px 8px;
  border-radius: 6px;
  width: 64px;
  text-align: center;
  font-weight: 600;
}

.size-input:focus {
  outline: none;
  box-shadow: 0 0 0 3px rgba(77, 144, 254, 0.12);
}
</style>
