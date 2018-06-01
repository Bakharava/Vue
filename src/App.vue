<template>
  <div id="app">
    <div class="main-container">
      <Header @newsUrlChange="changeNews"/>
      <Content :newsTypeParam="newsParam"/>
      <Footer/>
    </div>
  </div>
</template>

<script>
import Header from "./components/Header/Header";
import Content from "./components/ContentNews/Content";
import Footer from "./components/Footer/Footer";

export default {
  name: 'app',
  components: {
      Footer,
      Content,
      Header
  },
    data() {
      return {
          newsParam: ''
      }
    },
    methods: {
      changeNews(newsType) {
          return this.newsParam = newsType
      }
    }
}
</script>

<style src="./app.less"></style>
