<template>
  <div>
    <button class="btn">
      <slot></slot>
    </button>
  </div>
</template>

<script>
export default {
  name: "my-button",
};
</script>

<style lang="css" scoped>
.btn {
  margin-top: 12px;
  padding: 8px 8px;
  border: 1px solid rgb(224, 228, 229);
  border-radius: 12px;
  background-color: none;
  width: 150px;
  height: 40px;
  
}
.btn:hover{
  background-color: rgb(130, 148, 235);
  transition:  .3s;
}
</style>
