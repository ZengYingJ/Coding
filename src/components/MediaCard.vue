<template>
    <div class="media-card">
        <video v-if="type === 'video'" class="media-video" :src="src" autoplay webkit-playsinline loop></video>
        <img v-else-if="type === 'image'" class="media-image" :src="src" alt="cover">

        <slot></slot>
    </div>
</template>

<script>
export default {
    name: "MediaCard",
    props: {
        type: String,
        src: String,
    }
}
</script>

<style lang="less" scoped>
.media-card{
    position: relative;
    width: 100%;
    height: 100%;
    overflow: hidden;
    cursor: pointer;

    .media-video{
        position: relative;
        width: 100%;
        height: 100%;
    }
    .media-image{
        position: relative;
        display: block;
        width: 100%;
        height: 100%;
        object-fit: cover;
        transition: all .2s linear;
    }
    &:hover > .media-image{
        transform: scale(1.1);
        transform-origin: center;
    }
}
</style>