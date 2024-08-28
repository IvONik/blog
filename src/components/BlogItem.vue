<template>
  <div>
    <transition-group name="fade" tag="div">
      <div class="item" v-for="(item, index) in blogList" :key="item.id">
        <div class="title">
          {{ item.title }}
          <div
            @click="counter(item.id)"
            class="heart"
            :class="{ setLike: likedPosts.includes(item.id) }"
          >
            ❤{{ item.like }}
          </div>
        </div>

        <div class="body">
          {{ item.body }}
          <div class="button">
            <my-button @click="remove(item.id)" class="deletebtn">
              Удалить
            </my-button>
          </div>
        </div>
      </div>
    </transition-group>
  </div>
</template>

<script>
export default {
  data() {
    return {
      likedItemId: null,
    };
  },
  props: {
    blogList: {
      type: Array,
      required: true,
    },
    likedPosts: {
      type: Array,
      required: true,
    },
  },
  methods: {
    remove(id) {
      this.$emit("removePost", id);
    },
    counter(id) {
      this.$emit("addLikedPosts", id);
    },
  },
};
</script>

<style scoped>
.title {
  background-color: rgb(227, 235, 238);
  display: flex;
  justify-content: space-between;
  width: 500px;
  height: 20px;
  border: 2px solid rgb(224, 228, 229);
  border-radius: 12px 12px 0 0;
  padding: 12px;
  font-size: large;
}

.body {
  display: flex;
  flex-direction: column;
  width: 500px;
  border: 2px solid rgb(224, 228, 229);
  border-radius: 0 0 12px 12px;
  padding: 12px;
  margin-bottom: 16px;
}

.heart {
  cursor: pointer;
  color: grey;
  font-size: 20px;
  margin-left: 10px;
  transition: transform 0.3s;
}

.heart:hover {
  transform: scale(1.2);
}

.setLike {
  color: rgb(243, 97, 97);
}

.deletebtn {
  display: flex;
  justify-content: flex-end;
  right: 10px;
  bottom: 10px;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s, transform 0.5s;
}

.fade-enter, .fade-leave-to{
  opacity: 0;
  transform: translateX(-20px);
}
</style>
