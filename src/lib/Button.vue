<template>
  <button class="run-button" :class="classes" :disabled="disabled">
    <span v-if="loading" class="run-loadingIndicator"></span>
    <slot />
  </button>
</template>

<script lang="ts">
import { computed } from "vue";

export default {
  props: {
    theme: {
      type: String,
      default: "button",
    },
    size: {
      type: String,
      default: "normal",
    },
    level: {
      type: String,
      default: "normal",
    },
    disabled: {
      type: Boolean,
      default: false,
    },
    loading: {
      type: Boolean,
      default: false,
    },
  },
  setup(props) {
    const { theme, size, level } = props;
    const classes = computed(() => {
      return [`run-theme-${theme}`, `run-size-${size}`, `run-level-${level}`];
    });
    return { classes };
  },
};
</script>

<style lang="scss" scoped>
$h: 32px;
$border-color: #d9d9d9;
$color: #333;
// $green: #40a9ff;
$green: #925ee7;
$red: red;
$grey: grey;
$radius: 4px;

.run-button {
  box-sizing: border-box;
  height: $h;
  padding: 0 12px;
  cursor: pointer;
  display: inline-flex;
  justify-content: center;
  align-items: center;
  white-space: nowrap;
  background: white;
  color: $color;
  border: 1px solid $border-color;
  border-radius: $radius;
  box-shadow: 0 1px 0 fade-out(black, 0.95);
  transition: background 250ms;

  & + & {
    margin-left: 8px;
  }

  &:hover,
  &:focus {
    color: $green;
    border-color: $green;
  }

  &:focus {
    outline: none;
  }

  // 针对 Firefox 浏览器的优化
  &::-moz-focus-inner {
    border: 0;
  }

  &.run-theme-link {
    border-color: transparent;
    box-shadow: none;
    color: $green;
    &:hover,
    &focus {
      color: lighten($green, 10%);
    }
  }

  &.run-theme-text {
    border-color: transparent;
    box-shadow: none;
    color: inherit;
    &:hover,
    &:focus {
      background: darken(white, 5%);
    }
  }

  &.run-size-big {
    font-size: 24px;
    height: 48px;
    padding: 0 16px;
  }

  &.run-size-small {
    font-size: 12px;
    height: 20px;
    padding: 0 4px;
  }

  &.run-theme-button {
    &.run-level-main {
      background: $green;
      border-color: $green;
      color: white;
      &:hover,
      &:focus {
        background: darken($green, 10%);
        border-color: darken($green, 10%);
      }
    }

    &.run-level-danger {
      background: $red;
      border-color: $red;
      color: white;
      &:hover,
      &:focus {
        background: darken($red, 10%);
        border-color: darken($red, 10%);
      }
    }
  }

  &.run-theme-link {
    &.run-level-danger {
      color: $red;
      &:hover,
      &focus {
        color: darken($red, 10%);
      }
    }
  }

  &.run-theme-text {
    &.run-level-main {
      color: $green;
      &:hover,
      &focus {
        color: darken($green, 10%);
      }
    }

    &.run-level-danger {
      color: $red;
      &:hover,
      &:focus {
        color: darken($red, 10%);
      }
    }
  }

  &.run-theme-button {
    &[disabled] {
      cursor: not-allowed;
      color: $grey;
      &:hover {
        border-color: $grey;
      }
    }
  }

  &.run-theme-link,
  &.run-theme-text {
    &[disabled] {
      cursor: not-allowed;
      color: $grey;
    }
  }

  > .run-loadingIndicator {
    width: 10px;
    height: 10px;
    display: inline-block;
    margin-right: 4px;
    border-radius: 8px;
    border-color: $green $green $green transparent;
    border-style: solid;
    border-width: 2px;
    animation: run-spin 1s infinite linear;
  }
}

@keyframes run-spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
