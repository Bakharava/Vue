<template>
    <div class="content">
        <div class="content__wrapper">
            <div class="content__news">
                <div class="content__news-latest">
                    <div class="content__news-latest-text">Latest posts</div>
                </div>
                <div class="content__news-posts"></div>
                <div class="pagination">
                </div>
            </div>
            <div class="content__weather">
                <div class="weather-widget">
                    <!-- weather widget start --><a target="_blank" href="http://www.booked.net/weather/gomel-w631696">
                    <img src="https://w.bookcdn.com/weather/picture/11_w631696_1_1_ffffff_118_18acb4_999999_ffffff_1_ffffff_999999_0_6.png?scode=124&domid=w209&anc_id=59702"  alt="booked.net"/>
                </a><!-- weather widget end -->
                </div>
            </div>

        </div>
    </div>
</template>

<script>
    export default {
        name: "Content"
    }
</script>

<style src="./Content.less"></style>
