<template>
    <div class="pagination">
        <a v-bind:class="['pagination__page', page === isActive? 'active' : '', 'number'+page]"
           :key="page"
           v-for="page in getPagesAmount"
            @click="getActivePage(page)"
        >{{page}}</a>
    </div>
</template>

<script>
    export default {
        name: "Pagination",
        props: ['allNewsLength'],
        data() {
            return {
                pages: [],
                isActive: 1
            }
        },
        computed: {
            getPagesAmount() {
                let pagesAmount = Math.ceil(this.allNewsLength / 20);
                for (let i = 0; i < pagesAmount; i++) {
                    this.pages.push(i+1)
                }
                return this.pages;
            }
        },
        mounted() {
            this.getPagesAmount();
        },
        methods: {
            getActivePage(page) {
                this.$emit('activePageChanged', page);
                this.isActive = page;
            }
        }
    }
</script>

<style src="./Pagination.less"></style>
