<template>
  <section class="container">
    <div>
      <ul>
        <li><nuxt-link to="/login">ログインページへ</nuxt-link></li>
        <li><nuxt-link to="/authed-route">認証が必要なページへ</nuxt-link></li>
      </ul>
    </div>
    <div>
      <h3>Nuxt.jsのタグがつけられた投稿の一覧</h3>
      <ul>
        <li v-for="item in items" :key="item.id">
          <h4>
            <span>{{item.title}} </span>
            <small>
              <span>by </span>
              <nuxt-link :to="`/users/${item.user.id}`">
                {{item.user.id}}
              </nuxt-link>
            </small>
          </h4>
          <div>{{item.body.slice(0, 130)}}...</div>
          <p><a :href="item.url">{{item.url}}</a></p>
        </li>
      </ul>
    </div>
  </section>
</template>

<script>
import { mapGetters } from 'vuex'

export default {
  async asyncData({ store }) {
    if (store.getters['items'].length) {
      return
    }
    await store.dispatch('fetchItems')
  },
  computed: {
    ...mapGetters(['items'])
  }
}
</script>