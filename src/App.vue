<template>
  <div id="app">
    <div class="app__phone">
      <div class="phone__header">
        <div
          class="cancel__cta"
          v-if="step == 2 || step == 3"
          @click="toHome"
        >Cancel</div>
        <img src="./assets/vue_gram_logo_cp.png">
        <div
          class="next__cta"
          @click="next"
          v-if="step == 2"
        >Next</div>
        <div
          class="next__cta"
          @click="share"
          v-if="step == 3"
        >
          Share
        </div>
      </div>
      <app-phone-body
        :posts="postData"
        :step="step"
        :baseImg="result"
        :filterName="filterName"
        :filters="filters"
        v-model="caption"
      >
      </app-phone-body>
      <div class="phone__footer">
        <div
          class="home__cta"
          @click="toHome"
        >
          <i class="fas fa-home fa-lg"></i>
        </div>
        <div class="upload__cta">
          <input
            type="file"
            id="file"
            name="file"
            @change="upload"
            :disabled="step == 2 || step == 3"
          >
          <label for="file">
            <i class="far fa-plus-square fa-lg"></i>
          </label>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import phoneBody from './components/phoneBody.vue';
import postData from './data/posts.js';
import filters from './data/filters.js';
import eventBus from './event-bus.js';
export default {
  data() {
    return {
      postData: postData,
      filters: filters,
      step: 1,
      filterName: '',
      result: '',
      caption: ''
    }
  },
  created() {
    eventBus.$on('changeFilter', name => {
      this.filterName = name;
    })
  },
  methods: {
    upload(evt) {
      const files = evt.target.files;
      if(!files.length) {
        return;
      }
      if(files[0].type.indexOf('image') == -1) {
        return;
      }
      this.step = 2;
      const fileReader = new FileReader();
      fileReader.readAsDataURL(files[0])
      fileReader.onload = ext => {
        this.result = ext.target.result
      }
    },
    next() {
      this.step = 3;
    },
    share() {
      const shareData = {
        username: 'Shifeifei',
        userImage: "https://s3-us-west-2.amazonaws.com/s.cdpn.io/1211695/me2.png",
        postImage: this.result,
        likes: 0,
        hasBeenLiked: false,
        caption: this.caption,
        filter: this.filterName
      }
      this.postData.unshift(shareData);
      this.toHome();
    },
    toHome() {
      this.step = 1;
      this.filterName = '';
      this.caption = '';
      this.result = '';
    }
  },
  components: {
    appPhoneBody: phoneBody
  }
}
</script>

<style lang="scss" src="./styles/app.scss">

</style>
