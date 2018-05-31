<template>
    <div class="wrapper">
        <div class="header">
            <div class="header__link">
                <div class="header__logo">logo</div>
                <div class="header__link-news" >
                    <!--<a class="fa fa-home link-home"></a>-->
                    <a class="type active"
                       v-for="type in newsType"
                       :key="type"
                       @click="getNewsType(type)">
                        {{type}}
                    </a>
                </div>
                <div class="header__link-social">
                    <form class="search-news" target="_self">
                        <input id="search-news-input" type="search" autocomplete="off">
                    </form>
                    <a class="fa fa-twitter" href="https://www.twitter.com/" target="_blank"></a>
                    <a class="fa fa-pinterest" href="https://www.pinterest.com/" target="_blank"></a>
                    <a class="fa fa-facebook" href="https://www.facebook.com/" target="_blank"></a>
                    <a class="fa fa-instagram" href="https://www.instagram.com/" target="_blank"></a>
                </div>
            </div>
        </div>
        <SubHeader/>
    </div>
</template>

<script>
    import SubHeader from "./SubHeader/SubHeader";
    export default {
        name: "Header",
        components: {SubHeader},
        data() {
            return{
                newsType:["in world", "sport", "music", "business"],
                newsUrl: ''
            }
        },
        methods: {
            getNewsType(type) {
                this.$emit('newsUrlChange', type)
            }
        }
    }
</script>

<style src="./Header.less"></style>
