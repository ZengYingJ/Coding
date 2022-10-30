<template>
    <div class="page-banner">
        <div class="swiper">
            <template v-for="(item, idx) in bannerList">
                <div :class="{'swiper-item': true, show: currentBannerIndex === idx }" :key="item.url" @click="alertTitle(item.title)">
                    <img class="swiper-item-img" :src="item.url" :alt="item.title">
                </div>
            </template>

            <div class="swiper-pagination">
                <div class="swiper-pagination-button button-pre" @click="onPre">
                    <i class="eui-icon eui-icon-arrow-left"></i>
                </div>

                <ul class="swiper-pagination-list">
                    <template v-for="(item, idx) in bannerList">
                        <li :class="{ 'swiper-pagination-item': true, 'swiper-pagination-button': true, active: currentBannerIndex === idx }" 
                            :key="item.title"
                            @click="onSwiperHandle(idx)">{{ item.title }}</li>
                    </template>
                </ul>

                <div class="swiper-pagination-button button-next" @click="onNext">
                    <i class="eui-icon eui-icon-arrow-right"></i>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "PageBanner",
    data() {
        return {
            currentBannerIndex: 0,
            bannerList: [
                { title: "第四届追梦营", url: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20220909_2huzgbj4onv.png" },
                { title: "深圳创客节创意编程赛", url: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20221017_i1n62bthmuobanner.png" },
                { title: "深圳TGE虚拟机器人挑战赛", url: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20220901_rz0z7qqh2gtgebanner.jpg" },
                { title: "编程与人工智能活动", url: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20220909_9e0choci7rg_20220909101245.jpg" },
                { title: "腾讯游戏年度故事片", url: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20211230_u9kh06gxj4a79e15a997c42203c515773168a900f9.jpg" },
            ]
        }
    },
    mounted() {
        this.startBannerLoop();
    },
    destroyed() {
        if(this.bannerLoopInt){
            clearTimeout(this.bannerLoopInt);
        }
    },
    methods: {
        onSwiperHandle(idx) {
            clearTimeout(this.bannerLoopInt);
            this.currentBannerIndex = idx;

            this.startBannerLoop();
        },
        onNext() {
            clearTimeout(this.bannerLoopInt);

            if(this.currentBannerIndex + 1 >= this.bannerList.length){
                this.currentBannerIndex = 0;
            }else{
                this.currentBannerIndex++;
            }

            this.startBannerLoop();
        },
        onPre() {
            clearTimeout(this.bannerLoopInt);

            if(this.currentBannerIndex - 1 < 0){
                this.currentBannerIndex = this.bannerList.length - 1;
            }else{
                this.currentBannerIndex--;
            }

            this.startBannerLoop();
        },

        startBannerLoop() {
            this.bannerLoopInt = setTimeout(() => {
                this.onNext();
            }, 5000);
        },

        alertTitle(title) {
            alert(title);
        }
    }
}
</script>

<style lang="less" scoped>
@import "@/common/theme.less";

.page-banner{
    position: relative;
    width: 100%;
    height: 480px;
    background-color: @banner-bg-color;
    padding-top: 0;

    .swiper{
        position: absolute;
        left: 0;
        top: 0;
        width: 100%;
        height: 100%;

        .swiper-item{
            position: absolute;
            left: 0;
            top: 0;
            width: 100%;
            transition: all .5s linear;
            opacity: 0;
            z-index: 0;
            cursor: pointer;

            .swiper-item-img{
                position: relative;
                display: block;
                max-width: 100%;
                margin: 0 auto;
                object-fit: cover;
                object-position: center;
            }

            &.show{
                opacity: 1;
                z-index: 1;
            }
        }

        .swiper-pagination{
            position: absolute;
            z-index: 5;
            left: 50%;
            bottom: 0;
            display: flex;
            align-items: center;
            width: @screen-min-width;
            height: 50px;
            border-radius: 12px 12px 0 0;
            overflow: hidden;
            background-color: rgba(255, 255, 255, .8);
            transform: translateX(-50%);
            
            .swiper-pagination-button{
                position: relative;
                cursor: pointer;

                &::after{
                    position: absolute;
                    content: "";
                    left: 0;
                    bottom: 0;
                    width: 100%;
                    height: 6px;
                    background-image: linear-gradient(rgba(255, 255, 255, 0), rgba(0, 0, 0, 0.1));
                }

                &.active{
                    color: @secondary-color;
                    &::after{
                        height: 3px;
                        background-image: linear-gradient(@secondary-color, @secondary-color);
                    }
                }
            }

            .button-pre,
            .button-next{
                width: 50px;
                line-height: 50px;
                text-align: center;

                &:hover{
                    background-color: white;
                    & > .eui-icon{
                        color: @secondary-color !important;
                    }
                }
            }
            .button-pre{
                border-right: 1px solid rgba(255, 255, 255, .6);
            }

            .swiper-pagination-list{
                position: relative;
                display: flex;
                align-items: center;
                flex: 1;

                .swiper-pagination-item{
                    flex: 1;
                    line-height: 50px;
                    text-align: center;
                    border-right: 1px solid rgba(255, 255, 255, .6);

                    &:hover{
                        color: @secondary-color !important;
                    }
                }
            }
        }
    }
}

@media (max-width: 1920px) {
    .page-banner{
        height: auto;
        padding-top: 25%;
    }
}
</style>