<template>
  <div>
    <select :value="modelValue" @change="changeOption">
      <option value="" disabled>Cортировка</option>
      <option
        v-for="(item, index) in options"
        :key="item.value"
        :value="item.value"
      >
        {{ item.name }}
      </option>
    </select>
  </div>
</template>

<script>
export default {
  name: "my__sort",
  props: {
    modelValue: String,
    options: {
      type: Array,
      default: () => [],
    },
  },
  methods: {
    changeOption(event) {
      this.$emit("update:modelValue", event.target.value);
    },
  },
};
</script>

<style lang="css" scoped>
select {
  margin-top: 12px;
  padding: 10px 15px;
  border: 1px solid rgb(224, 228, 229);
  background-color: none;
  border-radius: 12px;
  width: 150px;
  height: 40px;
}
</style>
