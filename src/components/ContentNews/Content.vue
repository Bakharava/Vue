<template>
    <div class="content" id="posts">
        <div class="content__wrapper">
            <div class="content__news">
                <div class="content__news-latest">
                    <div class="content__news-latest-text">Latest posts</div>
                </div>
                <div class="content__news-posts">
                    <NewsCard :key="article.id" v-for="article in result" :article="article"/>
                </div>
                <Pagination/>
            </div>
            <div class="content__weather">
                <div class="weather-widget">
                    <!-- weather widget start --><a target="_blank" href="http://www.booked.net/weather/gomel-w631696">
                    <img src="https://w.bookcdn.com/weather/picture/11_w631696_1_1_ffffff_118_18acb4_999999_ffffff_1_ffffff_999999_0_6.png?scode=124&domid=w209&anc_id=59702"
                         alt="booked.net"/>
                </a><!-- weather widget end -->
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import axios from 'axios';
    import NewsCard from "../NewsCard/NewsCard";
    import Pagination from "../Pagination/Pagination";

 //   let newsUrlParam = 'sources=bbc-news,the-next-web,the-verge';
    const apiKey = 'b8d411a4e22745308fab1a665115c094';
    //let searchNewsParam = '';
    let pageNumberParam = '1';

    export default {
        name: "Content",
        components: {Pagination, NewsCard},
        props: ['newsTypeParam'],
        data() {
            return {
                result: [],
                loading: true,
                newsUrlParam: 'sources=bbc-news,the-next-web,the-verge',

            }
        },
   /*     computed: {
            updateNews() {
                if(this.newsTypeParam && this.newsTypeParam !== 'in world'){
                   return {
                       newsUrlParam:`category=${this.newsTypeParam}`
                   }
                }
            }
        },*/
        mounted() {
            this.getNews(this.newsUrlParam);
        },
        methods: {
            getNews(param) {
                const newsUrl = `https://newsapi.org/v2/top-headlines?${param}&language=en&pageSize=20&page=${pageNumberParam}&apiKey=${apiKey}`;
                axios.get(newsUrl).then(response => {
                    this.loading = false;
                    this.result = response.data.articles;
                }).catch((error) => {
                    console.log(error);
                });
            }
        },
   /*     watch:{
            newsUrlParam: function (newVal) {
                console.log(newVal)
                if(newVal) {
                    let param = newVal
                    this.getNews(param);
                }
            }
        }*/
     /*   updated() {
            let param = this.newsTypeParam === 'in world' ? this.newsUrlParam : `category=${this.newsTypeParam}`
            this.getNews(param);
        }*/
    };

</script>

<style src="./Content.less"></style>
