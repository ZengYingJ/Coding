<template>
    <header class="home-header">
		<div class="home-header-logo">
            <div class="logo logo-tgdp"></div>
            <span class="home-header-logo-divider"></span>
            <div class="logo logo-coding"></div>
		</div>

		<ul class="home-header-menu">
            <template v-for="(item) in navTopMenuList">
                <li :class="{'home-header-menu-item': true, 'active': !!item.active}" 
                    :key="item.title"
                    @click="alertTitle(item.title)"
                >{{ item.title }}</li>
            </template>
		</ul>

        <div class="home-header-actions">
            <div class="home-header-button">
                <div class="button-create">立即创作</div>

                <div class="home-header-dropdown">
                    <ul class="home-header-dropdown-list">
                        <template v-for="(item) in dropdownMenuList">
                            <li class="home-header-dropdown-item" :key="item.title" @click="alertTitle(item.title)">{{ item.title }}</li>
                        </template>
                    </ul>
                </div>
            </div>
            <div class="button-login">登录</div>
        </div>
	</header>
</template>

<script>
export default {
    name: "PageHeader",
    data() {
        return {
            navTopMenuList: [
                { title: "首页", active: true, },
                { title: "实验室" },
                { title: "课程" },
                { title: "名师团" },
                { title: "校园" },
                { title: "社区" },
                { title: "追梦营" },
                { title: "CodingDay" },
                { title: "赛事活动" },
            ],
            dropdownMenuList: [
                { title: "创意实验室" },
                { title: "Python实验室" },
                { title: "3D实验室" },
                { title: "人工智能实验室" },
                { title: "游戏实验室" },
                { title: "艺术(p5)实验室" },
                { title: "硬件实验室" },
                { title: "JS实验室" },
            ],
        }
    },
    methods: {
        alertTitle(title) {
            alert(title);
        },
    }
}
</script>


<style lang="less" scoped>
@import "@/common/theme.less";

.home-header{
    position: relative;
    display: flex;
    align-items: center;
    width: 100%;
    height: 60px;
    background-color: white;

    .home-header-logo{
        position: relative;
        display: flex;
        align-items: center;
        padding-left: 40px;

        .home-header-logo-divider{
            position: relative;
            display: block;
            width: 1px;
            height: 25px;
            margin: 0 10px;
            background-color: @divider-color;
        }
        .logo{
            position: relative;
            background-size: 100% 100%;

            &.logo-tgdp{
                width: 180px;
                height: 52px;
                background-image: url("https://coding.qq.com/packages/ecNavigationHeader/2.1.2-alpha.1/dist/2611814e22a171d522f9.png");
            }
            &.logo-coding{
                width: 133px;
                height: 57px;
                background-image: url(@logo-coding-small);
            }
        }
    }

    .home-header-menu{
        position: relative;
        display: flex;
        flex-wrap: wrap;
        align-items: center;
        margin-left: 20px;

        .home-header-menu-item{
            position: relative;
            padding: 0 28px;
            line-height: 42px;
            border-radius: 26px;
            transition: all 200ms linear;
            cursor: pointer;

            &.active{
                font-weight: bold;
                color: @primary-color;
            }
            &:hover{
                background-color: @divider-color;
            }
        }

        @media (max-width: 1450px) {
            .home-header-menu-item{
                padding: 0 15px;
            }
        }
    }

    .home-header-actions{
        position: absolute;
        top: 0;
        right: 40px;
        display: flex;
        align-items: center;
        height: 100%;

        .home-header-button{
            position: relative;

            .button-create{
                position: relative;
                width: 112px;
                line-height: 34px;
                font-size: 16px;
                text-align: center;
                background-color: @primary-color;
                color: white;
                border-radius: 17px;
                cursor: pointer;

                &::after{
                    position: relative;
                    content: '';
                    border-style: solid;
                    border-width: 6px 4px 0 4px;
                    border-color: #fff transparent transparent transparent;
                    display: inline-block;
                    margin-left: 6px;
                    transition: all 200ms;
                    vertical-align: 2px;
                }
                &:hover::after{
                    transform: rotate(180deg);
                }
            }

            .home-header-dropdown{
                position: absolute;
                display: none;
                z-index: 1000;
                width: 178px;
                top: 36px;
                left: 50%;
                transform: translateX(-50%);
                background-color: white;
                border-radius: 8px;
                box-shadow: 0 4px 20px @box-shadow-color;

                &::after{
                    position: absolute;
                    content: "";
                    top: -6px;
                    left: 50%;
                    border-style: solid;
                    border-width: 0 10px 6px 10px;
                    border-color: transparent transparent white transparent;
                    transform: translateX(-50%);
                }

                .home-header-dropdown-list{
                    position: relative;

                    .home-header-dropdown-item{
                        position: relative;
                        line-height: 43px;
                        padding: 0 20px;
                        font-size: 14px;
                        cursor: pointer;

                        &:hover{
                            color: @primary-color;
                            background-color: @divider-color;
                        }
                    }
                }
            }

            &:hover > .home-header-dropdown{
                display: block;
            }
        }
        .button-login{
            position: relative;
            line-height: 60px;
            margin-left: 20px;
            cursor: pointer;
        }
    }
}
</style>