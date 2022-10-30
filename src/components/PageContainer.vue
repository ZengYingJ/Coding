<template>
    <div class="page-container">
        <div class="page-container-inner">
            <div class="page-container-top">
                <!-- 编程好工具，学习更轻松 -->
                <p class="page-container-title">{{ title }}</p>
                <!-- 选择适合你的编程神器 -->
                <span class="page-container-subtitle">{{ subtitle }}</span>
            </div>

            <slot></slot>
        </div>
    </div>
</template>

<script>
export default {
    name: "PageContainer",
    props: {
        title: String,
        subtitle: String,
    }
}
</script>

<style lang="less" scoped>
@import "@/common/theme.less";

.page-container{
    position: relative;
    width: 100%;

    .page-container-inner{
        position: relative;
        width: @screen-min-width;
        margin: 0 auto;
        padding: 70px 0;  
        
        .page-container-top{
            position: relative;
            display: flex;
            flex-direction: column;
            align-items: center;
            margin-bottom: 26px;

            .page-container-title{
                font-size: 40px;
                font-weight: bold;
            }
            .page-container-subtitle{
                color: @font-color-gray;
            }
        }
    }
}
</style>