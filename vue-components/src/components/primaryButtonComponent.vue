<script setup>
import { ref } from 'vue';
const buttonText = ref('');
const clickCount = ref(0);
const isActive = ref(false);
const classArray = ref(['button', 'button--hyperion']);

const handleButtonClick = () => {
  buttonText.value = `Clicked ${++clickCount.value}`;
};

const handleError = () => {
  console.log({ ...classArray.value });
  // console.log(classArray.value);
};
</script>

<template>
  <button
    :class="[isActive ? classArray : 'button button--hyperion']"
    @click.capture.prevent="[isActive ? handleButtonClick() : handleError()]">
    <span
      ><span>{{ buttonText || 'Primary Button' }}</span></span
    >
  </button>
</template>

<style scoped>
.button {
  pointer-events: auto;
  cursor: pointer;
  background: #e7e7e7;
  border: none;
  padding: 1.5rem 3rem;
  margin: 0;
  font-family: inherit;
  font-size: inherit;
  position: relative;
  display: inline-block;
}

.button::before,
.button::after {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

.button--hyperion {
  font-family: input-mono-narrow, monospace;
  font-weight: 500;
  padding: 1rem 1.5rem;
  border: 1px solid #000;
  overflow: hidden;
  color: #fff;
}

.button--hyperion span {
  display: block;
  position: relative;
}

.button--hyperion > span {
  overflow: hidden;
}

.button--hyperion > span > span {
  overflow: hidden;
  mix-blend-mode: difference;
}

.button--hyperion:hover > span > span {
  animation: MoveUpInitial 0.2s forwards, MoveUpEnd 0.2s forwards 0.2s;
}

@keyframes MoveUpInitial {
  to {
    transform: translate3d(0, -105%, 0);
  }
}

@keyframes MoveUpEnd {
  from {
    transform: translate3d(0, 100%, 0);
  }
  to {
    transform: translate3d(0, 0, 0);
  }
}

.button--hyperion::before {
  content: '';
  background: #000;
  transition: transform 0.3s cubic-bezier(0.7, 0, 0.2, 1);
  transform-origin: 100% 50%;
}

.button--hyperion:hover::before {
  transform: scale3d(0, 1, 1);
  transform-origin: 0% 50%;
}
</style>
