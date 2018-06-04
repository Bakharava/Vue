<template>
    <div class="pagination">
        <a>&laquo;</a>
        <a v-bind:class="['pagination__page', page === isActive? 'active' : '', 'number'+page]"
           :key="page"
           v-for="page in changePagesAmount"
           @click="getActivePage(page)"
        >{{page}}</a>
        <a>&raquo;</a>
    </div>
</template>

<script>
    export default {
        name: "Pagination",
        props: ['allNewsLength'],
        data() {
            return {
                pages: [],
                isActive: 1,
                la: '&laquo'
            }
        },
        computed: {
            changePagesAmount() {
              return  this.getPagesAmount(this.allNewsLength)
            }
        },
        mounted() {
            this.getPagesAmount();
        },
        methods: {
            getActivePage(page) {
                this.$emit('activePageChanged', page);
                this.isActive = page;
            },
            getPagesAmount(ammount) {
                this.pages = [];
                let pagesAmount = Math.ceil(ammount / 20);
                for (let i = 0; i < pagesAmount; i++) {
                    this.pages.push(i+1);
                }
                return this.pages;
            }
        }
    }
</script>

<style src="./Pagination.less"></style>
