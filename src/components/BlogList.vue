<template>
  <div>
    <div class="btns">
      <my-button v-show="!showModalWindow" @click="showModal">
        Создать пост
      </my-button>

      <InputComp
        v-show="!showModalWindow"
        @find="updateSearchQuery"
        v-model="searchQuery"
      />
      <my-button @click="resetSearch" v-show="searchQuery" v-model="searchQuery"
        >Сбросить поиск</my-button
      >

      <my__sort v-model="selectedSort" :options="sortOptions" />
    </div>
    <PostForm
      v-show="showModalWindow"
      @createPost="createPost"
      @closeModalWindow="closeModalWindow"
    />
    <BlogItem
      :blogList="sortedBlogList"
      :likedPosts="likedPosts"
      @addLikedPosts="addLikedPosts"
      @removePost="removePost"
    />
  </div>
</template>

<script>
import BlogItem from "@/components/BlogItem.vue";
import PostForm from "@/components/PostForm.vue";
import InputComp from "@/components/InputComp.vue";

export default {
  components: {
    BlogItem,
    PostForm,
    InputComp,
  },
  data() {
    return {
      blogList: [
        {
          id: 1,
          title: "Bob Marley",
          body: "Lorem ipsum dolor sit amet consectetur adipisicing elit.",
          like: 0,
        },
        {
          id: 2,
          title: "Queen",
          body: "Lorem ipsum dolor sit amet consectetur adipisicing elit. Molestias consequatur, pariatur deserunt magnam quaerat dolorum sunt et aliquid illum, ducimus dolore expedita blanditiis! Sunt accusamus dolorem cum aliquam iste. Animi!",
          like: 0,
        },
        {
          id: 3,
          title: "Scorpions",
          body: "Lorem ipsum dolor sit amet consectetur adipisicing elit. Molestias consequatur, pariatur deserunt magnam quaerat dolorum sunt et aliquid illum, ducimus dolore expedita blanditiis!",
          like: 0,
        },
        {
          id: 4,
          title: "Imagine Dragons",
          body: "Lorem ipsum dolor sit amet consectetur adipisicing elit. Molestias consequatur, pariatur deserunt magnam quaerat dolorum sunt et aliquid illum.",
          like: 0,
        },
        {
          id: 5,
          title: "Bed Ford Falls",
          body: "Lorem ipsum dolor sit amet consectetur adipisicing elit. Molestias consequatur, pariatur deserunt magnam quaerat dolorum sunt et aliquid illum5.",
          like: 0,
        },
        {
          id: 6,
          title: "Pikovsky",
          body: "Lorem ipsum dolor sit amet consectetur adipisicing elit.",
          like: 3,
        },
      ],
      likedPosts: [ ],
      showModalWindow: false,
      searchQuery: "",
      selectedSort: "",
      sortOptions: [
        { value: "new", name: "сначала новые" },
        { value: "old", name: "сначала старые" },
      ],
    };
  },
  computed: {
    filteredBlogList() {
      if (this.searchQuery) {
        return this.blogList.filter(
          (obj) =>
            obj.title.toLowerCase().includes(this.searchQuery.toLowerCase()) ||
            obj.body.toLowerCase().includes(this.searchQuery.toLowerCase())
        );
      }
      return this.blogList;
    },
    sortedBlogList() {
      let sortedList = this.filteredBlogList.slice();
      if (this.selectedSort === "new") {
        sortedList.sort((a, b) => b.id - a.id);
      } else if (this.selectedSort === "old") {
        sortedList.sort((a, b) => a.id - b.id);
      }
      return sortedList;
    },
  },
  methods: {
    createPost(obj) {
      this.blogList.push(obj);
      this.showModalWindow = false;
    },
    removePost(id) {
      this.blogList = this.blogList.filter((elem) => elem.id !== id);
    },
    showModal() {
      this.showModalWindow = true;
    },
    closeModalWindow() {
      this.showModalWindow = false;
    },
    updateSearchQuery(query) {
      this.searchQuery = query;
    },
    resetSearch() {
      this.searchQuery = "";
    },
    addLikedPosts(id) {
      const index = this.likedPosts.indexOf(id);
      if (index !== -1) {
        this.likedPosts.splice(index, 1);
        this.updateLikes(id, -1);
      } else {
        this.likedPosts.push(id);
        this.updateLikes(id, 1);
      }
    },
    updateLikes(id, value) {
      const post = this.blogList.find(post => post.id === id);
      if (post) {
        post.like += value;
      }
    },
    },
};
</script>

<style scoped>
.btns {
  margin-bottom: 12px;
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  gap:16px;
}
</style>
