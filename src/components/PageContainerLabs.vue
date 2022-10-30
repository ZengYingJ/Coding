<template>
    <div class="page-container-labs">
        <page-container title="编程好工具，学习更轻松" subtitle="选择适合你的编程神器">
            <div class="page-container-panel">
                <div class="panel-aside">
                    <div class="panel-aside-list">
                        <ul class="panel-aside-list-inner" :style="labsContainerStyle">
                            <template v-for="(lab, lidx) in labs">
                                <li :class="{ 'panel-aside-item': true, 'active': lidx === curLabIdx }" 
                                    @mouseenter="onFocusAsideItem(lidx)" 
                                    @mouseleave="onBlurAsideItem()"
                                    @click="onClickAsideItem(lidx)"
                                    :key="lab.id">
                                    <div class="panel-aside-item-icon" :style="(lidx === curLabIdx || lidx === curHoverLabIdx) ? panelAsideItemIconStyle(lidx) : null">
                                        <img class="panel-aside-item-icon-img" :src="lab?.icon?.src" alt="icon">
                                    </div>
                                    <div class="panel-aside-item-content">
                                        <p class="panel-aside-item-title">{{ lab.title }}</p>
                                        <p class="panel-aside-item-subtitle">
                                            <template v-for="(tag) in lab.tags">
                                                <span class="panel-aside-item-tag" :key="tag">{{ tag }}</span>
                                            </template>
                                        </p>
                                    </div>
                                </li>
                            </template>
                        </ul>
                    </div>
                    <div class="panel-aside-more" @click="() => { this.firstPage = !this.firstPage }">
                        <i :class="{ 'eui-icon': true, 'eui-icon-arrow': true, 'active': !firstPage }"></i>
                    </div>
                </div>

                <div class="panel-main">
                    <div class="panel-main-content">
                        <div class="panel-main-content-info">
                            <p class="panel-main-content-subtitle">
                                <i class="iconhome iconhome-flag"></i>
                                <span>{{ labData.subtitle }}</span>
                            </p>
                            <p class="panel-main-content-title">{{ labData.title }}</p>
                            <p class="panel-main-content-desc">{{ labData.desc }}</p>
                            <div class="panel-main-content-actions">
                                <div class="panel-main-button-create">
                                    <i class="icon_qrcode" v-if="!!labData.qrcode"></i>
                                    <span>立即创作</span>

                                    <div class="panel-main-button-popover" v-if="!!labData.qrcode">
                                        <img class="panel-main-qrcode" :src="labData.qrcode" alt="qrcode">
                                        <span>扫码下载，立即体验</span>
                                    </div>
                                </div>
                                <div class="panel-main-button-more" v-if="!!labData.link">
                                    <span>了解更多</span>
                                    <i class="eui-icon eui-icon-arrow-right"></i>
                                </div>
                            </div>
                        </div>
                        <media-card class="panel-main-content-cover" :type="labData.mainMedia.type" :src="labData.mainMedia.src"></media-card>
                    </div>
                    <div class="panel-main-media" v-if="!!labData.exampleMedia">
                        <div class="panel-main-media-head">
                            <span>{{ labData.exampleMedia.exampleTitle }}</span>
                            <div class="panel-main-button-more" v-if="!!labData.exampleMedia.exampleLink">
                                <span>更多案例</span>
                                <i class="eui-icon eui-icon-arrow-right"></i>
                            </div>
                        </div>
                        <ul class="panel-main-media-list">
                            <template v-for="(item, idx) in labData.exampleMedia.list">
                                <li class="panel-main-media-item" :key="idx">
                                    <media-card class="panel-main-media-cover" :type="item.type" :src="item.src"></media-card>
                                    <p class="panel-main-media-item-title">{{ item.title }}</p>
                                </li>
                            </template>
                        </ul>
                    </div>
                </div>
            </div>
        </page-container>
    </div>
</template>

<script>
import PageContainer from '@/components/PageContainer';
import MediaCard from '@/components/MediaCard';

export default {
    name: "PageContainerLabs",
    components: {
        PageContainer,
        MediaCard,
    },
    data() {
        return {
            curLabIdx: 0,
            curHoverLabIdx: -1,
            firstPage: true,
            labs: [
                {
                    id: 1,
                    title: "创意实验室",
                    subtitle: "像搭积木一样编程创作",
                    desc: "让学编程和搭积木一样简单，有效帮助孩子形成编程思维，锻炼逻辑思维，轻松制作有趣有料的编程项目，发挥自己的无限创意。",
                    tags: ['6岁+', '创造力', '图形化'],
                    icon: {
                        color: "rgb(251, 232, 194)",
                        src: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200306_g9ofq50ftsdcreative.png",
                    },
                    qrcode: null,
                    link: "http://",
                    mainMedia: {
                        type: "video",
                        src: "https://wuji-30130.sz.gfp.tencent-cloud.com/20200323_8htrkrqaeb52.mp4",
                    },
                    exampleMedia: {
                        exampleTitle: "入门学习",
                        exampleLink: "http://",
                        list: [
                            {
                                type: "image",
                                title: "一起去郊游",
                                src: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200318_03b5pb9xb9xp.png",
                            },
                            {
                                type: "image",
                                title: "让贺卡动起来",
                                src: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200318_2058cxoa8hv.png",
                            },
                            {
                                type: "image",
                                title: "下雪吧",
                                src: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200318_1e0fz8k4etw.png",
                            }
                        ],
                    }
                },
                {
                    id: 2,
                    title: "Python实验室",
                    subtitle: "通用易懂的编程语言",
                    desc: "从图形化编程到文本编程，从AI应用到硬件物联，首创带有舞台区的编辑模式，运用动画和声音制作游戏，全方面体会Python语言的乐趣。",
                    tags: ["7岁+", "逻辑思维", "Python"],
                    icon: {
                        color: "rgb(193, 223, 251)",
                        src: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200306_7h0exzofi7tpython.png",
                    },
                    qrcode: null,
                    link: "http://",
                    mainMedia: {
                        type: "video",
                        src: "https://wuji-30130.sz.gfp.tencent-cloud.com/20200317_qrjirl2blsbpython.mp4",
                    },
                    exampleMedia: {
                        exampleTitle: "入门学习",
                        exampleLink: "http://",
                        list: [
                            {
                                type: "image",
                                title: "画星星",
                                src: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200318_7wbr2yla49.png",
                            },
                            {
                                type: "image",
                                title: "AI智能（语音+图像）",
                                src: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200318_5wctvliuxin.png",
                            },
                            {
                                type: "image",
                                title: "计算生日",
                                src: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200318_5hedqxj4g5c.png",
                            }
                        ],
                    }
                },
                {
                    id: 3,
                    title: "腾讯扣叮-编程第一课",
                    subtitle: "专为6-9岁孩子定制的编程启蒙App",
                    desc: "腾讯自研的游戏化编程启蒙APP，作为孩子的“编程第一课”，通过趣味的积木编程闯关，让孩子学习编程更简单、更有趣、更高效。",
                    tags: ["6-9岁", "编程启蒙", "计算思维"],
                    icon: {
                        color: "rgb(246, 202, 219)",
                        src: "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABoAAAAiCAYAAABBY8kOAAAEFElEQVRIia2XX0wcVRTGf3NnlyW0S11boLS1FhpLADXWKqCl0QbTmFRTNT5oYoyvuIkaEx/wyRfdN01MiL41vhijSY1SH7Q2TYWaUPoHWwoNVFppkQCtlUJhd2dmx9zZuduZ2eXf4vcyOefc+31z7px77h1tsu09lkEV8DLQCuwFtgApYBw4C/QA3wOTS9E4QtFEPC8w29HZBHwONC/3Ji56gXeiifjpAI/zFIVmzHZ0drgTVyqCO7bXnZuHUEDgEeALd4my0AWh+hpCjbXoD1YjysuwzQz2nTms8WnMS6OYQ1fByqgZn8x2dB4E2qOJ+EXlDAWUfSKh+h1EDrYiNm7wDdJ0Ha0ihqiIEX5sF5lbM6R+6sEcuqaG7HW5WnPv+0FtC5HnmmQ2HwJvZZkgcqCF0kPPoJWVLrtmckz40V1oIR1r9IZyb08f7zOBblQxAE8Dp9SIyIFmSvY/saxAIaRPnCH1S683IrP7XRXDp/eWq4aSZ4sTkZBzQw01XpfDLdx9ka0uXRB5cZ+zdEVDLvsL+xwuF5J7a8jdjNlsGmsRsWhOIjNxk+SRE2SmbiMqY5S+sh9RvWnZuOQINe7EvDCihr4kvJURbqj15bHw7a9YN6aw04bzlPZK42H/8rVKoSZliQeqfESZqX+KtsV2H1ez+kbZYPk6H7HcJ8XaIurj2iKFclvatm0fcemrbYjNG0HXnbWX9orjmq+iRMjtwg85QjNzaJvuy0X1bZWse/c1FsNScXtu3mtOyowuKysz/e+ipKuF9fdN74zzwj1PHJiXr62VP4cAV48UOpoL9g9jzyfXLCI5JJcHR6XQINDvDEgbwT5VFFLHeh0uF5J7UPWJ3GFlnB5wzphiYY5cx+gd8M52uJXQTM6taQhP5a0WemUMhO6ddckrlOve4d11iKr7ixbSNqwn/LCvlb2hhCqAFsclBCVtTxYtohDaXec1DymhN3MD6ncgYuVrF9q5LXhMhP3d+/G6RSevTklHW1/m9WyWQnuUpW+t/H+ELAv77oLXM13wXrcWAQmjbwhMS3nPAEl/Cxoec5723STmwJ+r1jH6R5j7+DDJH0963Z/h3ut+Bl6XRqqr29lw1pXraKUR52gPtHuM/mGs0XEizz+VdxWzRsaCXVverL7GrbqvgHNOJoaJefEK9kKKzO07GH+M4GfKkPrhJEbfIOnu876QPGKMwatBkXZlqG/UrsS8cDIcHssK35oh2dWNnUxnMzt1AeuvCcjYThYL3xwDw1Szz0YT8da8K7H7B7BntqOz2i33j4AG2YUXDncV/B4y+/kvjxSMAe8HHb6qiybiE9FE/Ds3w9zdtgDu9cZ8vB1NxH8Lupf6EZMNTwrKDOXuvuVWqLy8y58uFZPtSx6nKnY8jwn4DzeQgHU7MSGyAAAAAElFTkSuQmCC",
                    },
                    qrcode: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20210514_jwiemj3etneqrcode.png",
                    link: "http://",
                    mainMedia: {
                        type: "video",
                        src: "https://wuji-30130.sz.gfp.tencent-cloud.com/20210516_rfqbytd62t.MP4",
                    },
                    exampleMedia: {
                        exampleTitle: "应用截图",
                        exampleLink: null,
                        list: [
                            {
                                type: "image",
                                title: "妙趣剧情，学习不枯燥",
                                src: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20210514_667b2qum87qimg1.png",
                            },
                            {
                                type: "image",
                                title: "编程闯关，探索编程奥秘",
                                src: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20210516_8hkhp06cbfq04.png",
                            },
                            {
                                type: "image",
                                title: "知识解锁，收获丰富趣味知识",
                                src: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20210514_7xvlv329fmpimg3.png",
                            }
                        ],
                    }
                },
                {
                    id: 4,
                    title: "3D实验室",
                    subtitle: "创意实验室的3D版本",
                    desc: "扣叮和艾兰岛共同出品，学会了创意实验室就可以轻松上手，培养空间思维，制作3D创意作品。也可前往艾兰岛官网体验更专业的游戏编辑器。",
                    tags: ["6岁+", "创造力", "3D立体"],
                    icon: {
                        color: "rgb(187, 255, 245)",
                        src: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200429_ir7137irhcn48X48.png",
                    },
                    qrcode: null,
                    link: null,
                    mainMedia: {
                        type: "image",
                        src: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200429_1gi3qhorm28360X270.png",
                    },
                    exampleMedia: null,
                },
                {
                    id: 5,
                    title: "人工智能实验室",
                    subtitle: "算法模型，感受前沿科技p",
                    desc: "初学者直接应用简单的AI能力（拍照识花、语音识别、智能聊天等），体会AI的乐趣；高阶学习者参与常见算法模型的调参过程，学习AI的底层逻辑。",
                    tags: ["10+岁", "前沿科技", "走进AI"],
                    icon: {
                        color: "rgb(193, 244, 236)",
                        src: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200306_whgr206kz0sai.png",
                    },
                    qrcode: null,
                    link: "http://",
                    mainMedia: {
                        type: "video",
                        src: "https://wuji-30130.sz.gfp.tencent-cloud.com/20200317_ojl6d4y4ciq.mp4",
                    },
                    exampleMedia: {
                        exampleTitle: "入门学习",
                        exampleLink: "http://",
                        list: [
                            {
                                type: "image",
                                title: "姿态侦测",
                                src: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200318_f32mm1mf6bu.png",
                            },
                            {
                                type: "image",
                                title: "涂鸦",
                                src: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200318_zezz83b7i8s.png",
                            },
                            {
                                type: "image",
                                title: "智能聊天",
                                src: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200318_vqtfx8vb56t.png",
                            }
                        ],
                    }
                },
                {
                    id: 6,
                    title: "游戏实验室",
                    subtitle: "图形化编程，创意游戏闯关",
                    desc: "积木块拼接而成的丰富多彩的创意游戏世界，零基础小朋友也可以通过图形化编程进行寻路闯关。",
                    tags: ["6-8岁", "创意游戏", "零基础"],
                    icon: {
                        color: "rgb(220, 199, 251)",
                        src: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200306_16yws3wyo7hgame.png",
                    },
                    qrcode: null,
                    link: null,
                    mainMedia: {
                        type: "video",
                        src: "https://wuji-30130.sz.gfp.tencent-cloud.com/20200430_qdivvm8bin.mp4",
                    },
                    exampleMedia: null,
                },
                {
                    id: 7,
                    title: "艺术(p5)实验室",
                    subtitle: "用编程进行艺术表达",
                    desc: "将编程与艺术、数学等STEAM多方面知识相结合，制作可视化的艺术案例，激发学生的想象力和创造力，帮助更好地学习理解数理知识。",
                    tags: ["7+岁", "艺术表达", "数理知识"],
                    icon: {
                        color: "rgb(246, 202, 219)",
                        src: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200306_otye6yv5nvart.png",
                    },
                    qrcode: null,
                    link: "http://",
                    mainMedia: {
                        type: "video",
                        src: "https://wuji-30130.sz.gfp.tencent-cloud.com/20200430_nhuts1fwacd.mp4",
                    },
                    exampleMedia: {
                        exampleTitle: "入门学习",
                        exampleLink: "http://",
                        list: [
                            {
                                type: "image",
                                title: "蒙德里安",
                                src: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200319_tis672tlbb3.gif",
                            },
                            {
                                type: "image",
                                title: "wavemarker",
                                src: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200319_kmojlnizag1.gif",
                            },
                            {
                                type: "image",
                                title: "recursice tree",
                                src: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200319_1zhg4pshyjkh2.gif",
                            }
                        ],
                    }
                },
                {
                    id: 8,
                    title: "硬件实验室",
                    subtitle: "软硬件结合的编程体验",
                    desc: "通过在线编程，控制Arduino、micro:bit、OpenAIE、CocoRobo等教育硬件，并同时支持积木和代码两种模式，体会软硬结合的编程学习。",
                    tags: ["6+岁", "软硬结合", "创客教育"],
                    icon: {
                        color: "rgb(193, 244, 236)",
                        src: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200311_r7ymefinhg.png",
                    },
                    qrcode: null,
                    link: null,
                    mainMedia: {
                        type: "video",
                        src: "https://wuji-30130.sz.gfp.tencent-cloud.com/20200430_k5b1bg002nl.mp4",
                    },
                    exampleMedia: null,
                },
                {
                    id: 9,
                    title: "JS实验室",
                    subtitle: "面向对象的Web语言",
                    desc: "从积木命令到文本代码，从形状绘制到精灵动画，引导掌握计算机科学知识，从易到难感受JavaScript语言的魅力。",
                    tags: ["7+岁", "前端开发", "Javascript"],
                    icon: {
                        color: "rgb(251, 232, 194)",
                        src: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200311_8036tcku7o20200306_igf96a5gbzjs.png",
                    },
                    qrcode: null,
                    link: "http://",
                    mainMedia: {
                        type: "video",
                        src: "https://wuji-30130.sz.gfp.tencent-cloud.com/20200430_0kifyfeks6k.mp4",
                    },
                    exampleMedia: {
                        exampleTitle: "入门学习",
                        exampleLink: "http://",
                        list: [
                            {
                                type: "image",
                                title: "彩虹旗",
                                src: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200318_cp1j4hqdd.png",
                            },
                            {
                                type: "image",
                                title: "海底世界",
                                src: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200318_4cls7al5io1.png",
                            },
                            {
                                type: "image",
                                title: "绘制大世界",
                                src: "https://wuji-30130.sz.gfp.tencent-cloud.com/pics/20200318_jcw5u0z95y.png",
                            }
                        ],
                    }
                },
            ]
        }
    },
    computed: {
        labsContainerStyle() {
            return `transform: translateY(${this.firstPage ? 0 : -164}px)`;
        },
        labData() {
            return this.labs[this.curLabIdx];
        }
    },
    methods: {
        panelAsideItemIconStyle(lidx) {
            return `background-color: ${this.labs[lidx]?.icon?.color}`;
        },
        onFocusAsideItem(idx) {
            this.curHoverLabIdx = idx;
        },
        onBlurAsideItem() {
            this.curHoverLabIdx = -1;
        },
        onClickAsideItem(idx) {
            this.curLabIdx = idx;
        },
    }
}
</script>

<style lang="less" scoped>
@import "@/common/theme.less";

.page-container-labs{
    position: relative;
    width: 100%;

    .page-container-panel{
        position: relative;
        width: 100%;
        height: 600px;
        display: flex;
        border-radius: 12px;
        overflow: hidden;
        background-color: white;

        .panel-aside{
            position: relative;
            width: 290px;
            height: 100%;
            background-color: @secondary-color;

            @panel-aside-list-height: 574px;
            .panel-aside-list{
                position: relative;
                width: 100%;
                height: @panel-aside-list-height;
                overflow: hidden;

                .panel-aside-list-inner{
                    position: absolute;
                    left: 0;
                    top: 0;
                    width: 100%;
                    transition: all .2s linear;

                    .panel-aside-item{
                        position: relative;
                        display: flex;
                        align-items: center;
                        width: 100%;
                        height: 82px;
                        padding: 0 20px;
                        border-bottom: 1px solid @secondary-color;
                        color: white;
                        cursor: pointer;

                        .panel-aside-item-icon{
                            position: relative;
                            display: flex;
                            justify-content: center;
                            align-items: center;
                            width: 48px;
                            height: 48px;
                            background-color: white;
                            border-radius: 12px;
                            transition: all .2s linear;

                            .panel-aside-item-icon-img{
                                position: relative;
                                display: block;
                                transition: all .2s linear;
                            }
                        }
                        .panel-aside-item-content{
                            position: relative;
                            margin-left: 14px;
                            font-size: 18px;
                            color: white;

                            .panel-aside-item-title,
                            .panel-aside-item-subtitle{
                                position: relative;
                                width: 180px;
                                overflow: hidden;
                                text-overflow: ellipsis;
                                white-space: nowrap;

                                .panel-aside-item-tag:not(:last-of-type){
                                    margin-right: 4px;
                                }
                            }
                            .panel-aside-item-subtitle{
                                font-size: 12px;
                            }
                        }

                        &:hover{
                            color: @primary-color;
                            background-color: rgba(255, 255, 255, .1);

                            .panel-aside-item-icon{
                                border-radius: 50%;
                                .panel-aside-item-icon-img{
                                    transform: scale(0.9);
                                }
                            }
                            .panel-aside-item-content{
                                color: rgba(255, 255, 255, .8);
                            }
                        }
                        &.active{
                            background-color: white;
                            &::after{
                                position: absolute;
                                content: "";
                                left: 0;
                                top: 0;
                                width: 4px;
                                height: 100%;
                                background-color: @primary-color;
                            }
                            .panel-aside-item-icon{
                                border-radius: 50%;
                            }
                            .panel-aside-item-content{
                                color: @primary-color;
                            }
                        }
                    }
                }
            }
            .panel-aside-more{
                position: relative;
                height: calc(100% - @panel-aside-list-height);
                text-align: center;
                background-color: @primary-color;
                cursor: pointer;

                .eui-icon{
                    display: block;
                    font-size: 20px;
                    color: rgba(255, 255, 255, .5);
                    transform: rotate(180deg);
                    transition: all .2s linear;

                    &.active{
                        transform: rotate(0deg);
                    }
                }
                &:hover > .eui-icon{
                    color: white;   
                }
            }
        }
        .panel-main{
            position: relative;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            flex: 1;
            height: 100%;
            padding: 30px 50px;

            .panel-main-content{
                position: relative;
                display: flex;
                justify-content: space-between;
                width: 100%;
                padding-bottom: 20px;
                border-bottom: 1px solid @divider-color;

                .panel-main-content-info{
                    position: relative;
                    width: 410px;

                    .panel-main-content-subtitle{
                        position: relative;
                        display: flex;
                        align-items: center;
                        line-height: 30px;

                        .iconhome{
                            position: relative;
                            margin-right: 10px;
                            font-size: 24px;
                            color: @icon-yellow-color;
                        }
                    }
                    .panel-main-content-title{
                        position: relative;
                        font-size: 24px;
                        margin-top: 23px;
                    }
                    .panel-main-content-desc{
                        position: relative;
                        height: 90px;
                        margin-top: 12px;
                        line-height: 30px;
                        display: -webkit-box;
                        overflow: hidden;
                        text-overflow: ellipsis;
                        -webkit-box-orient: vertical;
                        -webkit-line-clamp: 3;
                        color: @font-color-gray;
                    }
                    .panel-main-content-actions{
                        position: relative;
                        display: flex;
                        align-items: center;
                        margin-top: 30px;

                        .panel-main-button-create{
                            position: relative;
                            display: flex;
                            align-items: center;
                            justify-content: center;
                            width: 150px;
                            height: 40px;
                            border-radius: 20px;
                            background-color: @primary-color;
                            color: white;
                            cursor: pointer;

                            &:hover{
                                background-color: @secondary-color;

                                .panel-main-button-popover{
                                    display: flex;
                                }
                            }
                            .icon_qrcode{
                                position: relative;
                                width: 14px;
                                height: 14px;
                                margin-right: 6px;
                                background-image: url(@icon-qrcode);
                                background-size: 100% 100%;
                            }
                            .panel-main-button-popover{
                                position: absolute;
                                z-index: 5;
                                bottom: 50px;
                                left: 50%;
                                width: 180px;
                                height: 214px;
                                display: none;
                                flex-direction: column;
                                justify-content: center;
                                align-items: center;
                                color: @font-color-gray;
                                border-radius: 12px;
                                box-shadow: 0 0 4px @box-shadow-color;
                                background-color: white;
                                transform: translateX(-50%);

                                .panel-main-qrcode{
                                    position: relative;
                                    display: block;
                                    width: 142px;
                                    height: 142px;
                                    margin-bottom: 10px;
                                }
                            }
                        }
                    }
                }
                .panel-main-content-cover{
                    position: relative;
                    width: 360px;
                    height: 270px;
                    border: 1px solid @divider-color;
                    border-radius: 8px;
                }
            }
            .panel-main-media{
                position: relative;
                width: 100%;
                padding-bottom: 10px;

                .panel-main-media-head{
                    position: relative;
                    display: flex;
                    justify-content: space-between;
                    align-items: center;
                    font-size: 18px;
                }
                .panel-main-media-list{
                    position: relative;
                    display: flex;
                    margin-top: 8px;

                    .panel-main-media-item{
                        position: relative;
                        display: flex;
                        flex-direction: column;
                        align-items: flex-start;

                        .panel-main-media-cover{
                            position: relative;
                            width: 258px;
                            height: 140px;
                            border-radius: 4px;
                        }
                        .panel-main-media-item-title{
                            position: relative;
                            margin-top: 8px;
                            overflow: hidden;
                            text-overflow: ellipsis;
                            white-space: nowrap;
                            cursor: pointer;

                            &:hover{
                                color: @primary-color;
                            }
                        }

                        &:not(:last-of-type){
                            margin-right: 18px;
                        }
                    }
                }
            }

            .panel-main-button-more{
                position: relative;
                display: flex;
                align-items: center;
                margin-left: 28px;
                font-size: 16px;
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
}
</style>