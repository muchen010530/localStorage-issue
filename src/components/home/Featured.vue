<template>
  <div class="featured">
    <title-view :label="titleText" :btn="btnText" v-if="titleVisible && data && data.length > 0"></title-view>
    <div class="featured-list">
      <div class="featured-item-wrapper">
        <div class="featured-item" v-for="(item, index) in data" :key="index" @click="showBookDetail(item)">
          <div class="img-wrapper">
            <img class="img" :src="item.cover">
          </div>
          <div class="content-wrapper">
            <div class="title" ref="title">{{item.title}}</div>
            <div class="author" ref="author">{{item.author}}</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  import TitleView from './Title'
  import { realPx } from '@/utils/utils'
  import { categoryText } from '../../utils/store'
  import { storeHomeMixin } from '../../utils/mixin'

  export default {
    mixins: [storeHomeMixin],
    components: {
      TitleView
    },
    props: {
      data: Array,
      titleVisible: {
        type: Boolean,
        default: true
      },
      titleText: {
        type: String
      },
      btnText: {
        type: String
      }
    },
    computed: {
      width() {
        return window.innerWidth - realPx(20) - realPx(60) + 'px'
      }
    },
    methods: {
      categoryText(category) {
        return categoryText(category, this)
      },
      resize() {
        this.$nextTick(() => {
          this.$refs.title.forEach(item => {
            item.style.width = this.width
          })
          this.$refs.author.forEach(item => {
            item.style.width = this.width
          })
          this.$refs.category.forEach(item => {
            item.style.width = this.width
          })
        })
      }
    }
  }
</script>

<style lang="scss" rel="stylesheet/scss" scoped>
  @import "../../assets/global";

  .featured {
    .featured-list {
      width: 100%;
      padding: 0 px2rem(10);
      box-sizing: border-box;
      .featured-item-wrapper {
        width: 100%;
        display: flex;
        flex-flow: row wrap;
        justify-content: flex-start;
        align-items: flex-start;
        .featured-item {
          flex: 0 0 100%;
          width: 100%;
          padding: px2rem(15) 0 0 ;
          @include top;
          .img-wrapper {
            flex: 0 0 30%;
            width: 30%;
            .img {
              border-radius: px2rem(8);
              width: 100%;
              // width: px2rem(50);
              // height: px2rem(75);
            }
          }
          .content-wrapper {
            flex: 1;
            width: px2rem(117.5);
            padding: 0 px2rem(5) 0  px2rem(10);
            box-sizing: border-box;

            .title{
              font-size: px2rem(15);
              margin-top: px2rem(10);
            }
            .author {
              font-size: px2rem(15);
              margin-top: px2rem(30);
            }
          }
        }
      }
    }
  }
</style>
