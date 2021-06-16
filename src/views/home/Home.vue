<template>
    <div id="home">
        <nav-bar class="home-nav"><div slot="center">购物车</div></nav-bar>

        <swiper>
            <swiper-item  v-for="item in banners" :key="item.label">
                <a :href="item.link">
                    <img :src="item.image" alt="">
                </a>
            </swiper-item>
        </swiper>

        <recommend-view :recommends="recommends"/>

        <feature-view/>

       <tab-control class="tab-control" :titles="['流行','新款','精选']"/>

        <goods-list :goods="goods['pop'].list"/>
    </div>
</template>

<script>
    import NavBar from "../../components/common/navbar/NavBar";

    import {Swiper,SwiperItem} from "components/common/swiper"
    import FeatureView from "./childComps/FeatureView";


    import RecommendView from "./childComps/RecommendView";

    import TabControl from "../../components/content/tabControl/TabControl";
    import GoodsList from "../../components/content/goods/GoodsList";
    import {getHomeMultidata,getHomeGoods} from "../../network/home";
    export default {
        name: "Home",
        components: {
            NavBar,
            Swiper,
            SwiperItem,
            RecommendView,
            FeatureView,
            TabControl,
            GoodsList
        },
        comments:{
            NavBar
        },
        data(){
            return{
                banners:[],
                recommends:[],
                good:{
                    "pop":{page:0,list:[]},
                    "news":{page:0,list:[]},
                    "sell":{page:0,list:[]},
                }
            }
        },
        created() {
            //1.请求多个数据
            this.getHomeMultidata()
            //2.请求商品数据
            this.getHomeGoods('pop')
            // this.getHomeGoods("new")
            // this.getHomeGoods("sell")

        },
        methods:{
            getHomeMultidata(){
                getHomeMultidata().then(res =>{
                  /*  console.log(res);*/
                    // this.result = res;
                    this.banners = res.data.banner.list;
                    this.recommends = res.data.recommend.list;
                })
            },
            getHomeGoods(type){
                const page = this.good[type].page + 1
                getHomeGoods(type,page).then(res =>{
                    console.log("kkkkkk",res);
                   /* this.goods[type].list.push(...res.data.list)
                    this.goods[type].page += 1*/
                })
            }
        }
    }
</script>

<style scoped>
    #home{
        padding-top: 44px;
    }
    .home-nav{
        background-color: var(--color-tint);
        color: #ffffff;

        position: fixed;
        left: 0;
        right: 0;
        top:0;
        z-index: 9;
    }
    .tab-control{
        position: sticky;
        top:44px;
        z-index: 9;
    }
</style>
