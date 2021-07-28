<template>
  <label
      class="b-contain"
      :style="cssProps"
      @click="$emit('hide-chart', idx, !checked)"
  >
    <span>{{ dataset.label }}</span>
    <input type="checkbox" id="checkbox" v-model="checked">
    <div class="b-input"></div>
  </label>
</template>

<script>
export default {
  name: "LegendItem",
  props: {
    dataset: {
      type: Object,
      required: true
    },
    color: {
      type: String,
    },
    idx: null
  },
  data: () => ({
    checked: true,
  }),
  computed: {
    cssProps() {
      return {
        '--checkbox-color': this.color,
      }
    }
  },
  mounted() {

  },
  methods: {

  }
}
</script>

<style scoped>
.b-contain *, .b-contain *::before, .b-contain *::after {
  box-sizing: content-box !important;
}

.b-contain input {
  position: absolute;
  z-index: -1;
  opacity: 0;
}

.b-contain span {
  line-height: 1.54;
  font-size: 1rem;
  font-family: inherit;
}

.b-contain {
  display: table;
  position: relative;
  padding-left: 1.8rem;
  cursor: pointer;
  margin-bottom: .5rem;
}

.b-contain input[type="checkbox"] ~ .b-input {
  position: absolute;
  top: 0;
  left: 0;
  height: 1.25rem;
  width: 1.25rem;
  background: aliceblue;
  transition: background 250ms;
  border: 1px solid var(--checkbox-color);
  border-radius: 0.3rem;
}

.b-contain input[type="checkbox"] ~ .b-input::after {
  content: '';
  position: absolute;
  display: none;
  left: .45rem;
  top: 0.09rem;
  width: .25rem;
  height: 0.79rem;
  border: solid var(--checkbox-color);
  border-width: 0 2px 2px 0;
  transition: background 250ms;
  transform: rotate(45deg);
}

.b-contain input:disabled ~ .b-input::after {
  border-color: rgba(135, 149, 161, 1);
}

.b-contain input:checked ~ .b-input::after {
  display: block;
}

.b-contain input:checked ~ .b-input {
  background: aliceblue;
  border-color: var(--checkbox-color);
}

.b-contain input[type="checkbox"]:disabled ~ .b-input {
  background: aliceblue;
  border-color: rgba(184, 194, 204, 1);
  opacity: 0.6;
  cursor: not-allowed;
}

.b-contain input:checked:focus ~ .b-input, .b-contain:hover input:not([disabled]):checked ~ .b-input {
  background: aliceblue;
  border-color: var(--checkbox-color);
}

.b-contain .b-input::before {
  content: '';
  display: none;
  position: absolute;
  left: 0;
  top: 0;
  width: 3rem;
  height: 3rem;
  margin-left: -0.85rem;
  margin-top: -0.85rem;
  background: var(--checkbox-color);
  border-radius: 2rem;
  opacity: .6;
  z-index: 99999;
  transform: scale(0);
}

.b-contain .b-input::before {
  visibility: hidden;
}

.b-contain input:focus + .b-input::before {
  visibility: visible;
}

.b-contain:first-child .b-input::before {
  visibility: hidden;
}
</style>
