<template>
  <Wrap :page="page">
    <div class="home">
      <h1 class="page-heading" v-if="page.attributes.title">{{ page.title }}</h1>

      <slot name="default"></slot>

      <h2
        class="post-list-heading"
        v-if="page.posts && page.posts.length > 0"
      >{{ page.attributes.listTitle || 'Posts' }}</h2>

      <ul class="post-list" v-if="page.posts && page.posts.length > 0">
        <li v-for="post in page.posts" :key="post.attributes.permalink">
          <span class="post-meta">{{ formatDate(post.attributes.createdAt) }}</span>
          <h3>
            <saber-link
              class="post-link"
              :to="post.attributes.permalink"
            >{{ post.attributes.title }}</saber-link>
          </h3>
        </li>
      </ul>

      <div
        class="pagination"
        v-if="page.pagination && (page.pagination.hasNext || page.pagination.hasPrev)"
      >
        <router-link
          class="prev-link"
          :to="page.pagination.prevLink"
          v-if="page.pagination.hasPrev"
        >← Previous</router-link>
        <router-link
          class="next-link"
          :to="page.pagination.nextLink"
          v-if="page.pagination.hasNext"
        >Next →</router-link>
      </div>

      <p class="feed-subscribe">
        <svg class="svg-icon orange">
          <use :xlink:href="getSvg('rss')"></use>
        </svg>
        <a :href="feedURL">Subscribe</a>
      </p>
    </div>
  </Wrap>
</template>

<script>
import { feedURL } from 'saber/variables'
import formatDate from '../src/utils/formatDate'
import Wrap from '../src/components/Wrap.vue'
import getSvg from '../src/utils/getSvg'

export default {
  components: {
    Wrap
  },

  props: ['page'],

  data() {
    return {
      feedURL
    }
  },

  methods: {
    formatDate,
    getSvg
  }
}
</script>
