<template lang="pug">
.single-page
  navigation-bar(title="我的心得")
  .content 
    review-item(v-for="r in myReviews", :key="r.id" :review="r.id")
        
</template>
<script>
import faker from 'faker'
import { mapState, mapActions } from 'vuex'
import ReviewItem from './ReviewItem'

export default {
  name: 'MyReview',
  components: {
    ReviewItem,
  },
  data() {
    return {
      // src: faker.image.avatar()
    }
  },
  created() {
    if (this.myReviews.length === 0) this.fetchReview()
  },
  computed: {
    ...mapState({
      reviews: (s) => s.review.reviews,
      ids: (s) => s.user.me.reviews,
    }),
    myReviews() {
      return this.ids.map((id) => this.reviews[id])
    },
  },
  methods: {
    ...mapActions({ fetchReview: 'review/fetchReview' }),
    // fetchReview() {
    //   this.$store.dispatch('review/fetchReview')
    // }

  },
}
</script>
<style lang="stylus" scoped>
.mine
  margin-bottom 0.2rem
  background-color #fff

.pic
  width 0.8rem
  height 0.8rem
  border-radius 50%
  vertical-align middle
  margin 0.2rem

.ni
  font-size 0.3rem

.comment
  font-size 0.2rem
  text-align left
  padding 0 0.2rem

.pictures
  padding 0.2rem

.picture
  width 2.6rem
  height 2rem

.product
  border 1px solid #f2f2f2
  display flex
  justify-content left
  align-items center
  padding 0.2rem

.image
  width 1rem
  height 1rem
  margin-right 0.5rem

.description
  text-align left
  font-size 0.2rem
  border-left 1px solid #f2f2f2
  padding 0 0.5rem

.description p
  padding 0.05rem 0
  margin 0

.description p:last-child
  color #f00

.other
  background-color #fff
</style>