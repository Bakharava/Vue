<template>
    <div class="newsCard">
        <a class="newsCard__link" :href="article.url" target="_blank">
            <img  class="newsCard__link-img" :src="article.urlToImage ? article.urlToImage : fakeImage" :alt="article.title">

            <div class="newsCard__news-title">{{article.title ? article.title : " "}}</div>
            <p class="newsCard__news-time">{{article.publishedAt ? article.publishedAt.replace(/[\T\Z]/g, ' ') : " "}}</p>

        </a>
    </div>
</template>

<script>

    export default {
        name: "NewsCard",
        props: ['article'],
        data() {
            return {
                fakeImage: "../../assets/image/news.jpg"
            };
        }
    }
</script>

<style src="./NewsCard.less"></style>
