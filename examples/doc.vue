<template>
  <main>
    <header>
      <i class="iconfont icon-logo"></i>
      <strong> FDK UI Components </strong>
    </header>
    <aside>
      <nav>
        <span v-for="item in nav[lang]" :key="item.id">
          <router-link
            v-if="item.path"
            :to="`/${lang+item.path}`">{{item.title}}</router-link>
          <em v-else>{{ item.name.toUpperCase() }}</em>
          <router-link
            v-for="(o, i) in item.list"
            :to="`/${lang+o.path}`"
            :key="i">{{o.title}}</router-link>
        </span>
      </nav>
    </aside>
    <router-view class="content"></router-view>
    <div class="examples">
      <iframe :src="demo" frameborder="0"></iframe>
    </div>
    <footer>Copyright &copy; 2017 JuFan FE</footer>
  </main>
</template>
<script>
import nav from './nav.json';

export default {
  name: 'app',
  data() {
    return {
      nav,
    };
  },
  computed: {
    lang() {
      const lang = this.$route.path.match(/\/([^/]+)/);
      return lang ? lang[1] : 'zh-CN';
    },
    demo() {
      return `/example/#${this.$route.path}`;
    },
  },
};

</script>
<style lang="postcss">
@import 'md';
@import 'icon';

main {
  display: grid;
  width: 100%;
  grid-template-rows: 50px auto 50px;
  grid-template-columns: 270px calc(100% - 700px)  395px;
  grid-column-gap: 20px;
  overflow-x: hidden;
  grid-template-areas: 'header header header' 'aside article examples' 'footer footer footer';
  header {
    grid-area: header;
    line-height: 47px;
    font-size: 16px;
    text-indent: 20px;
    background-color: #600;
    color: white;
    .icon-logo {
      margin-right: 10px;
      font-size: 32px;
      vertical-align: middle;
    }
    a {
      position: absolute;
      right: 20px;
      color: white;
    }
  }
  aside {
    grid-area: aside;
    line-height: 38px;
    border-right: 1px solid #ddd;
    nav {
      padding-top: 20px;
      padding-bottom: 80px;
      em {
        display: block;
        text-indent: 1em;
        font-size: 12px;
        opacity: .43;
        &~a {
          text-indent: 2em;
        }
      }
      a {
        display: block;
        text-indent: 1em;
        opacity: .5;
        color: #900;
        text-decoration: none;
        text-transform: capitalize;
        &.router-link-active {
          border-right: 2px solid rgba(150, 0, 0, .3);
          background-color: rgba(150, 0, 0, .1);
          opacity: 1;
        }
        &:hover {
          opacity: 1;
        }
      }
    }
  }
  .examples {
    grid-area: examples;
    iframe {
      position: fixed;
      top: 100px;
      right: 10px;
      width: 24%;
      height: 70%;
      /* width: 375px;
      height: 667px; */
      max-width: 375px;
      max-height: 667px;
      box-shadow: 0 0 6px rgba(0, 0, 0, .2);
    }
  }
  footer {
    grid-area: footer;
    line-height: 50px;
    text-align: center;
    background-color: #500;
    color: rgba(255, 255, 255, .7);
  }
}

</style>
