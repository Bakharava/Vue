<template>
    <div class="wrapper">
        <div class="header">
            <div class="header__link">
                <div class="header__logo">logo</div>
                <div class="header__link-news">
                    <!--<a class="fa fa-home link-home"></a>-->
                    <a class="active" id="1">in world</a>
                    <a id="2">sport</a>
                    <a id="3">music</a>
                    <a id="4">business</a>
                    <!-- <a> blog</a>-->
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
        props: {
            msg: String
        }
    }
</script>

<style src="./Header.less"></style>
