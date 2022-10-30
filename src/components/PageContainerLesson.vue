<template>
    <div class="page-container-lesson">
        <page-container title="趣味课程，名师名家带你学" subtitle="学习丰富的权威认证课程">
            <div class="page-container-panel">
                <ul class="panel-tab-list">
                    <template v-for="(tab, tidx) in lessons">
                        <li :class="{ 'panel-tab-item': true, active: tidx === curLessonIdx }" 
                            :key="tidx"
                            @click="onChangeTab(tidx)">{{ tab.tabName }}</li>
                    </template>
                </ul>

                <ul class="panel-main">
                    <template v-for="(lesson, lidx) in curLessonList">
                        <li class="panel-main-media" :key="lidx">
                            <media-card class="panel-main-media-cover" type="image" :src="lesson.cover">
                                <span :class="`panel-main-media-cover-tag ${lesson.tag}`">{{ getLessonTagString(lesson.tag) }}</span>
                            </media-card>
                            <p class="panel-main-media-title">{{ lesson.title }}</p>
                        </li>
                    </template>
                </ul>

                <div class="panel-button-more">
                    <span>更多课程</span>
                    <i class="eui-icon eui-icon-arrow-right"></i>
                </div>
            </div>
        </page-container>
    </div>
</template>

<script>
import PageContainer from "@/components/PageContainer";
import MediaCard from '@/components/MediaCard';

export default {
    name: "PageContainerLesson",
    components: {
        PageContainer,
        MediaCard,
    },
    computed: {
        curLessonList() {
            return this.lessons[this.curLessonIdx].list;
        },
    },
    data() {
        return {
            curLessonIdx: 0,
            lessons: [
                {
                    tabName: "编辑推荐",
                    list: [
                        {
                            tag: "easy",
                            cover: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200925_ley7xak5xfl.jpg",
                            title: "神奇的画板",                            
                        },
                        {
                            tag: "easy",
                            cover: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200929_ljjstzp9asc.jpg",
                            title: "发射器的密码",   
                        },
                        {
                            tag: "easy",
                            cover: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200911_9ppjd7xydg6.jpg",
                            title: "趣味打气球",
                        },
                        {
                            tag: "easy",
                            cover: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200831_2qquh3nmog8.png",
                            title: "初代益智休闲游戏：俄罗斯方块（上集）",
                        },
                        {
                            tag: "easy",
                            cover: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200925_bxz2eqa09cq.jpg",
                            title: "球球大作战",
                        },
                        {
                            tag: "easy",
                            cover: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200909_999y6omn98u.jpg",
                            title: "航天器发射计划",
                        },
                        {
                            tag: "easy",
                            cover: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200925_cdxn2wractu.jpg",
                            title: "扣叮音乐节",
                        },
                        {
                            tag: "easy",
                            cover: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200929_ee0bgh5wel5.png",
                            title: "斐波那契数列",
                        }
                    ]
                },
                {
                    tabName: "低年级（三年级或以下）",
                    list: [
                        {
                            tag: "easy",
                            cover: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200318_3vvqgnboy37.png",
                            title: "一起去郊游",                            
                        },
                        {
                            tag: "easy",
                            cover: "https://p.qpic.cn/qqgameedu/0/3d331987fa9216a04cf5435ab3d2b07c/0",
                            title: "贪吃鸡",   
                        },
                        {
                            tag: "easy",
                            cover: "https://p.qpic.cn/qqgameedu/0/9f9957f843abe3a29ec671f6162ed392/0",
                            title: "科普八大行星",
                        },
                        {
                            tag: "easy",
                            cover: "https://p.qpic.cn/qqgameedu/0/f63787a90f25c088e813e1d3ac8444bb/0",
                            title: "一起舞蹈吧",
                        },
                        {
                            tag: "easy",
                            cover: "https://p.qpic.cn/qqgameedu/0/b3aceefa13fcf0e08b674693ad1b93ff/0",
                            title: "小火车",
                        },
                        {
                            tag: "easy",
                            cover: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200318_q9imnokbxt.png",
                            title: "马达动起来",
                        },
                        {
                            tag: "easy",
                            cover: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200318_rf46gppvaaf.png",
                            title: "JS实验室绘图",
                        },
                        {
                            tag: "easy",
                            cover: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200318_bi5mqf656yu.png",
                            title: "米老鼠拓展课（一）",
                        }
                    ]
                },
                {
                    tabName: "高年级（四年级或以上）",
                    list: [
                        {
                            tag: "easy",
                            cover: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200318_fv4dtm89rf4.png",
                            title: "欢乐打地鼠",                            
                        },
                        {
                            tag: "medium",
                            cover: "https://p.qpic.cn/qqgameedu/0/41d677564ffeed6110f452f70c691d66/0",
                            title: "保卫农场",   
                        },
                        {
                            tag: "easy",
                            cover: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200318_2ldwryeur4j.png",
                            title: "旋转摩天轮",
                        },
                        {
                            tag: "medium",
                            cover: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200318_5ev5qjofm5u.png",
                            title: "开动汽车",
                        },
                        {
                            tag: "medium",
                            cover: "https://p.qpic.cn/qqgameedu/0/57f1729002eb5790f335a8b6aad03fda/0",
                            title: "躲避陨石",
                        },
                        {
                            tag: "easy",
                            cover: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200318_s2e1kqnvox.png",
                            title: "埃舍尔视觉错觉作品",
                        },
                        {
                            tag: "easy",
                            cover: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200608_232p1644um8.png",
                            title: "Python-Turtle 初识",
                        },
                        {
                            tag: "easy",
                            cover: "https://p.qpic.cn/qqgameedu/0/9f9957f843abe3a29ec671f6162ed392/0",
                            title: "科普八大行星",
                        }
                    ]
                },
                {
                    tabName: "初中及以上",
                    list: [
                        {
                            tag: "medium",
                            cover: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200318_c22d8kc2e5f.png",
                            title: "白细胞大作战",                            
                        },
                        {
                            tag: "hard",
                            cover: "https://p.qpic.cn/qqgameedu/0/36a6d292401611680aa1276ceaa4c094/0",
                            title: "月球采矿任务",   
                        },
                        {
                            tag: "medium",
                            cover: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200318_vz2jmyadnh.png",
                            title: "消防车出击",
                        },
                        {
                            tag: "hard",
                            cover: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200318_ydi6ow891s.png",
                            title: "救援大行动",
                        },
                        {
                            tag: "medium",
                            cover: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200318_1dgvn8qg7zz.png",
                            title: "其他输入",
                        },
                        {
                            tag: "hard",
                            cover: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200318_ixi5o7a3whl.png",
                            title: "项目：互动贺卡",
                        },
                        {
                            tag: "medium",
                            cover: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200805_r500sw89gxj.png",
                            title: "摘苹果",
                        },
                        {
                            tag: "hard",
                            cover: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200805_hbff6k2i34.jpg",
                            title: "小猫钓鱼",
                        }
                    ]
                },
            ]
        }
    },
    methods: {
        onChangeTab(idx) {
            this.curLessonIdx = idx;
        },
        getLessonTagString(tag) {
            switch(tag){
                case "easy":
                    return "简单";
                case "medium":
                    return "中等";
                case "hard":
                    return "困难";
            }
        }
    }
}
</script>

<style lang="less" scoped>
@import "@/common/theme.less";

.page-container-lesson{
    position: relative;
    background-color: white;

    .page-container-panel{
        position: relative;
        display: flex;
        flex-direction: column;
        align-items: center;

        .panel-tab-list{
            position: relative;
            display: flex;
            align-items: center;

            .panel-tab-item{
                position: relative;
                line-height: 34px;
                margin: 0 10px;
                padding: 0 20px;
                text-align: center;
                border-radius: 17px;
                background-color: @background-color;
                cursor: pointer;

                &:hover{
                    color: @primary-color;
                }
                &.active{
                    background-color: @primary-color;
                    color: white;
                }
            }
        }
        .panel-main{
            position: relative;
            width: 100%;
            display: flex;
            flex-wrap: wrap;
            justify-content: space-between;
            margin-top: 40px;

            .panel-main-media{
                position: relative;
                display: flex;
                flex-direction: column;
                align-items: flex-start;
                width: 288px;
                margin-bottom: 40px;

                .panel-main-media-cover{
                    position: relative;
                    width: 100%;
                    height: 226px;
                    overflow: hidden;
                    border-radius: 4px;

                    .panel-main-media-cover-tag{
                        position: absolute;
                        z-index: 1;
                        left: 10px;
                        top: 10px;
                        width: 50px;
                        line-height: 22px;
                        text-align: center;
                        font-size: 14px;
                        color: white;
                        box-shadow: 0 2px 5px @box-shadow-color;
                        border-radius: 2px 11px 11px 2px;

                        &.easy{
                            background-color: @tag-green-color;
                        }
                        &.medium{
                            background-color: @tag-orange-color;
                        }
                        &.hard{
                            background-color: @tag-purple-color;
                        }
                    }
                }
                .panel-main-media-title{
                    position: relative;
                    margin-top: 12px;
                    overflow: hidden;
                    text-overflow: ellipsis;
                    white-space: nowrap;
                    cursor: pointer;

                    &:hover{
                        color: @primary-color;
                    }
                }
            }
        }
        .panel-button-more{
            position: relative;
            display: flex;
            align-items: center;
            cursor: pointer;

            .eui-icon{
                margin-left: 6px;
                font-size: 12px;
                color: @font-color;
            }
            &:hover {
                color: @primary-color;
                .eui-icon{
                    color: @primary-color;
                }
            }
        }
    }
}
</style>