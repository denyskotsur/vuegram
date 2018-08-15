<template>
  <div id="app">
    <div class="app-phone">
      <phone-header :step="step"
                    :onCancelHandler="goToHome"
                    :onNextHandler="() => step++"
                    :onShareHandler="sharePost" />
      <phone-body :posts="posts"
                  :filters="filters"
                  :step="step"
                  :image="image"
                  :selectedFilter="selectedFilter"
                  v-model="caption" />
      <phone-footer :onUploadImage="uploadImage"
                    :goHomeHandler="goToHome"
                    :step="step" />
    </div>
  </div>
</template>

<script>
import PhoneBody from "./components/PhoneBody";
import PhoneHeader from "./components/PhoneHeader";
import PhoneFooter from "./components/PhoneFooter";

import posts from "./data/posts";
import filters from "./data/filters";

import EventBus from "./event-bus";

export default {
  name: "App",

  components: {
    "phone-body": PhoneBody,
    "phone-header": PhoneHeader,
    "phone-footer": PhoneFooter
  },

  data() {
    return {
      posts,
      filters,
      step: 1,
      image: "",
      selectedFilter: "",
      caption: ""
    };
  },

  methods: {
    uploadImage(evt) {
      const files = evt.target.files;
      if (!files.length) return;
      const reader = new FileReader();
      reader.readAsDataURL(files[0]);
      reader.onload = evt => {
        this.image = evt.target.result;
        this.step = 2;
      };
      // To enable reuploading of same files in Chrome
      document.querySelector("#file").value = "";
    },

    goToHome() {
      this.image = "";
      this.selectedFilter = "";
      this.caption = "";
      this.step = 1;
    },

    sharePost() {
      const post = {
        username: "fullstack_vue",
        userImage:
          "https://s3-us-west-2.amazonaws.com/s.cdpn.io/1211695/vue_lg_bg.png",
        postImage: this.image,
        likes: 0,
        caption: this.caption,
        filter: this.filterType
      };
      this.posts.unshift(post);
      this.goToHome();
    }
  },

  created() {
    EventBus.$on("filter-selected", evt => {
      this.selectedFilter = evt.filter;
    });
  }
};
</script>

<style lang="scss" src="./styles/app.scss">
// Styles from stylesheet
</style>