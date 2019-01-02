<template>
  <section class="container">
    <h2>NEWS</h2>
    <ul>
      <li v-for="post in all" :key="post.date">
        <nuxt-link :to="post._path">
          {{ post.title }}
        </nuxt-link>
      </li>
    </ul>
    <ul>
      <li v-for="post in blog" :key="post.date">
        <nuxt-link :to="post._path">
          {{ post.title }}
        </nuxt-link>
      </li>
    </ul>
    <ul>
      <li v-for="post in test" :key="post.date">
        <nuxt-link :to="post._path">
          {{ post.title }}
        </nuxt-link>
      </li>
    </ul>
  </section>
</template>

<script>
import AppLogo from '~/components/AppLogo.vue';

export default {
  components: {
    AppLogo
  },
  data() {
    // Using webpacks context to gather all files from a folder
    // const context = require.context('~/content/blog/posts/', false, /\.json$/);
    //
    // const posts = context.keys().map(key => ({
    //   ...context(key),
    //   _path: `/blog/${key.replace('.json', '').replace('./', '')}`,
    // }));

    const blogContext = require.context('~/content/blog/posts/', false, /\.json$/);
    const blog = blogContext.keys().map(key => ({
      ...blogContext(key),
      _path: `/blog/${key.replace('.json', '').replace('./', '')}`,
    }));

    const testContext = require.context('~/content/test/posts/', false, /\.json$/);
    const test = testContext.keys().map(key => ({
      ...testContext(key),
      _path: `/test/${key.replace('.json', '').replace('./', '')}`,
    }));

    return {
      blog,
      test,
      all: [
        ...blog,
        ...test
      ]
    };
  }
};
</script>

<style>
.container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif; /* 1 */
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
