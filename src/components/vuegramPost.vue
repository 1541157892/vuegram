<template>
  <div class="vuegram__post">
    <div class="header level">
      <div class="level-left">
        <figure class="image is-32x32">
          <img :src="postData.userImage">
        </figure>
        <span class="username">{{ postData.username }}</span>
      </div>
    </div>
    <div
      class="image__container"
      :class="postData.filter"
      @dblclick="watchLike"
      :style="{backgroundImage: 'url(' + postData.postImage + ')'}"
    ></div>
    <div class="content">
      <div class="heart">
        <i
            @click="watchLike"
            :class="{fas: this.postData.hasBeenLiked}"
            class="far fa-heart"></i>
      </div>
      <p class="likes">{{ postData.likes }}</p>
      <p class="caption">
        <span>{{ postData.username }}</span>
        {{postData.caption}}
      </p>
    </div>
  </div>
</template>

<script>
export default {
    props: {
        posts: {
            type: Object
        }
    },
    data() {
        return {
            postData: this.posts
        }
    },
    methods: {
        watchLike() {
            this.postData.hasBeenLiked ? --this.postData.likes : ++this.postData.likes
            this.postData.hasBeenLiked = !this.postData.hasBeenLiked;
        }
    },
};
</script>

<style lang="scss" src="../styles/vuegram-post.scss">
</style>
