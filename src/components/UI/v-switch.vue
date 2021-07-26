<template>
  <div class="v-switch">
    <span
        class="v-switch-wrapper"
        role="checkbox"
        tabindex="0"
        @click="toggle"
        @keydown.space.prevent="toggle"
    >
      <span
        class="v-switch-background"
      />
      <span
        class="v-switch-indicator"
        :style="indicatorStyles"
      />
    </span>
  </div>
</template>

<script>
export default {
  name: 'v-switch',

  props: {
    typeSearch:{
      type: Boolean,
      default: true
    }
  },

  computed: {
    indicatorStyles() {
      return { transform: this.typeSearch ? 'translateX(20px)' : 'translateX(0)' };
    }
  },

  methods: {
    toggle() {
      this.$emit('change-type-search', !this.typeSearch);
    }
  }
};
</script>

<style>
.v-switch {
  margin: 0 12px;
}

.v-switch-wrapper {
  display: inline-block;
  position: relative;
  cursor: pointer;
  width: 40px;
  height: 24px;
  border-radius: 9999px;
}

.v-switch-wrapper:focus {
  outline: 0;
}

.v-switch-background {
  display: inline-block;
  border-radius: 9999px;
  height: 100%;
  width: 100%;
  box-shadow: inset 0 2px 4px rgba(0, 0, 0, 0.1);
  transition: background-color .4s ease;
  background-color: #3d9967;
}

.v-switch-indicator {
  position: absolute;
  height: 17px;
  width: 17px;
  left: 2px;
  bottom: 4px;
  background-color: #ffffff;
  border-radius: 9999px;
  box-shadow:  0 2px 4px rgba(0, 0, 0, 0.1);
  transition: transform .4s ease;
}
</style>
