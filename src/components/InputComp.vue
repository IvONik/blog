<template>
  <div>
    <input
      type="text"
      :value="modelValue"
      @input="$emit('update:modelValue', $event.target.value)"
      placeholder="search..."
    />
  </div>
</template>

<script>
export default {
  props: {
    modelValue: {
      type: String,
      required: true,
    },
  },
};
</script>
<style lang="css" scoped>
input{
    margin-top: 12px;
    padding: 10px 15px;
    border: 1px solid rgb(224, 228, 229);
    border-radius: 12px;
    background-color: none;
    max-width: 110px;
    font-size: 16px;
}
</style>

