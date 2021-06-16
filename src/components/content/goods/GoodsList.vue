<template>
    <div class="goods">
        <goods-list-item v-for="item in goods" :key="item.label" :goods-item="item"/>

    </div>
</template>

<script>
    import GoodsListItem from "./GoodsListItem";
    export default {
        name: "GoodsList",
        component: {
            GoodsListItem
        },
        props:{
            goods:{
                type:Array,
                default(){
                    return[]
                }
            }
        }
    }
</script>

<style scoped>
    .goods{
        display: flex;
        flex-wrap: wrap;
        justify-content: space-around;
    }
</style>