<template>
  <div class="phone__body">
    <div class="feed" v-dragscroll>
      <transition-group name="fade" tag="div">
        <div v-if="step == 1" :key="step">
          <app-vuegram-post
              v-for="(post, key) in posts"
              :key="key"
              :posts="post"
          ></app-vuegram-post>
        </div>
        <div v-else-if="step == 2" :key="step">
          <app-filter
              :filters="filters"
              :baseImg="baseImg"
              :filterName="filterName"
          ></app-filter>
        </div>
        <div v-else :key="step">
            <div
              class="selected__image"
              :class="filterName"
              :style="{backgroundImage: 'url(' + baseImg + ')'}"
            >
            </div>
            <div class="caption__container">
                <textarea
                  placeholder="Write a caption"
                  :value="value"
                  @input="changeCaption"
                ></textarea>
            </div>
        </div>
      </transition-group>
    </div>
  </div>
</template>

<script>
import vuegramPost from "./vuegramPost";
import filterType from './filterType';
export default {
  data() {
    return {
      ftName: this.filterName
    }
  },
  props: {
    value: {
        type: String
    },
    filterName: {
        type: String
    },
    filters: {
      type: Array
    },
    baseImg: {
      type: String
    },
    step: {
      type: Number
    },
    posts: {
      type: Array
    }
  },
  methods: {
      changeCaption(evt) {
          this.$emit('input', evt.target.value);
      }
  },
  components: {
    appVuegramPost: vuegramPost,
    appFilter: filterType
  }
};
</script>

<style lang="scss" src="../styles/phone-body.scss">
</style>
<style lang="scss" src="../styles/filter-type.scss">
</style>
<style lang="scss" src="../styles/transition.scss">
</style>
