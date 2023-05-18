<template>
  <button class="btn">
    Join Now
    <ArrowRight />
  </button>
</template>

<script>
import ArrowRight from './icons/ArrowRight.vue'
export default {
  components: {
    ArrowRight
  }
}
</script>

<style scoped>
.btn {
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  outline: none;
  padding: 12px 20px;
  gap: 8px;
  background: #15141b;
  border: none;
  box-shadow: 0px 1px 2px rgba(16, 24, 40, 0.05);
  border-radius: 8px;
  font-weight: 500;
  font-size: 16px;
  line-height: 24px;
  /* identical to box height, or 150% */
  width: 100%;
  color: #667085;
}
.btn:hover {
  background: #21202b;
  color: #ffffff;
}
</style>
