<template>
  <div>
    <button class="button" @click="$emit('click', $event)"><slot /></button>
  </div>
</template>

<script lang="ts">
export default {};
</script>

<style lang="scss" scoped>
.button {
  background: orangered;
  color: white;
  border-radius: 4px;
  border: none;
  &-wrapper {
    text-align: center;
    padding: 16px;
    margin-top: 28px;
  }
}
</style>