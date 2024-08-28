<template>
  <div class="overlay" @click.self="$emit('closeModalWindow')">
    <div class="box">
      <input v-model="title" type="text" class="title" placeholder="Заголовок" />
      <textarea v-model="body" class="body" placeholder="Текст"></textarea>
      <my-button @click="create">Создать</my-button>
      <!-- <my-button @click="closeModal">Отмена</my-button> -->
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: "",
      body: "",
    };
  },
  props: {
    show: Boolean,
  },
  methods: {
    create() {
      if (this.title && this.body) {
        const obj = {
          id: new Date(),
          title: this.title,
          body: this.body,
          like: 0,
        };
        this.$emit("createPost", obj);
        this.title = "";
        this.body = "";
      }
    },
  },
};
</script>

<style scoped>
.overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.3);
  display: flex;
  justify-content: center;
  align-items: center;
}

.box {
  width: 500px;
  height: 400px;
  background-color: #fff;
  border: 2px solid gray;
  border-radius: 12px;
  padding: 12px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  /* -webkit-box-shadow: 4px 4px 22px 0px rgba(34, 60, 80, 0.42);
  -moz-box-shadow: 4px 4px 22px 0px rgba(34, 60, 80, 0.42);
  box-shadow: 4px 4px 22px 0px rgba(34, 60, 80, 0.42); */
}

.title {
  width: 300px;
  height: 32px;
  border-radius: 12px 12px 0 0;
  margin-bottom: 8px;
  background-color: bisque;
  padding: 12px;
  border: 1px solid gray;
}

.body {
  width: 300px;
  height: 300px;
  border-radius: 0 0 12px 12px;
  margin-bottom: 8px;
  background-color: bisque;
  padding: 12px;
}
</style>

