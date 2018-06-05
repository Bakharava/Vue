<template>
    <div class="content" id="posts">
        <div class="content__wrapper">
            <div class="content__news">
                <div class="content__news-latest">
                    <div class="content__news-latest-text">Latest posts</div>
                </div>
                <div class="content__news-posts" v-if="!loading">
                    <NewsCard :key="article.id" v-for="article in result" :article="article"/>
                </div>
                <Loader v-if="loading"/>
                <Pagination
                        :allNewsLength="allNewsLength"
                        :pageSize="pageSize"
                        @activePageChanged="changePage"/>
            </div>
            <div class="content__additional">
                <div class="weather-widget">
                    <Weather />
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import axios from 'axios';
    import NewsCard from "../NewsCard/NewsCard";
    import Pagination from "../Pagination/Pagination";
    import Loader from "../Loader/Loader";
    import { EventBus } from "../EventBus";
    import Weather from "../Weather/Weather";

    const apiKey = 'b8d411a4e22745308fab1a665115c094';
    //let searchNewsParam = '';

    export default {
        name: "Content",
        components: {Weather, Pagination, NewsCard, Loader},
       // props: ['newsTypeParam'],
        data() {
            return {
                result: [],
                allNewsLength: '',
                loading: true,
                newsUrlParam: 'top-headlines?sources=bbc-news,the-next-web,the-verge',
                pageNumberParam: 1,
                pageSize: 20
            }
        },
        mounted() {
            this.getNews(this.newsUrlParam);
        },
        created() {
            EventBus.$on('newsUrlChange', (type) => {
                this.pageNumberParam = 1;
                this.newsUrlParam = type === 'in world' ? this.newsUrlParam : `top-headlines?category=${type}`;
                this.getNews(this.newsUrlParam);
            });
            EventBus.$on('getSearchNews', searchParams => {
               const param = `everything?q=${searchParams}`;
                this.getNews(param);
            })
        },
        methods: {
            getNews(param) {
                const newsUrl = `https://newsapi.org/v2/${param}&language=en&pageSize=${this.pageSize}&page=${this.pageNumberParam}&apiKey=${apiKey}`;
                axios.get(newsUrl).then(response => {
                    this.loading = false;
                    this.result = response.data.articles;
                    this.allNewsLength = response.data.totalResults;
                }).catch((error) => {
                    console.log(error);
                });
            },
            changePage(page) {
                this.pageNumberParam = page;
                this.getNews(this.newsUrlParam)
            }
        }
    };

</script>

<style src="./Content.less"></style>
