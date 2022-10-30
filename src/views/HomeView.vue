<template>
	<div class="home">
		<page-header></page-header>
		<page-banner></page-banner>

		<div class="notice">
			<i class="icon-notice"></i>
			<span class="notice-content" @click="alertMessage(noticeContent)">{{ noticeContent }}</span>
			<i class="icon-hot">Hot</i>
		</div>

		<page-container-labs id="labs"></page-container-labs>
		<page-container-lesson id="lessons"></page-container-lesson>

		<page-footer></page-footer>

		<div :class="{ 'sidebar-fixed': true, visible: sidebarVisible }">
			<ul class="sidebar-list">
				<template v-for="(bar) in sidebarList">
					<li :class="{ 'sidebar-item': true, active: bar.id === curSidebarId }" :key="bar.id" @click="onHandleSideBar(bar.id)">
						<i :class="`sidebaricon ${bar.icon}`"></i>
						<span>{{ bar.label }}</span>
					</li>
				</template>
			</ul>
		</div>
	</div>
</template>

<script>
import PageHeader from "@/components/PageHeader";
import PageBanner from "@/components/PageBanner";
import PageContainerLabs from "@/components/PageContainerLabs";
import PageContainerLesson from "@/components/PageContainerLesson";
import PageFooter from "@/components/PageFooter";

const noticeContentList = [
	"立项四年，腾讯互娱如何做编程教育",
	"2021腾讯追梦营嘉年华圆满落幕",
	"腾讯编程课进村，这是孩子们创作的“APP”",
]

export default {
	name: "HomeView",
	components: {
		PageHeader,
		PageBanner,
		PageContainerLabs,
		PageContainerLesson,
		PageFooter,
	},
	data() {
		return {
			noticeContent: "立项四年，腾讯互娱如何做编程教育",
			sidebarVisible: false,
			sidebarList: [
				{ icon: "sidebaricon-labs", label: "实验室", id: "labs" },
				{ icon: "sidebaricon-course", label: "学好课", id: "lessons" },
				{ icon: "sidebaricon-top", label: "回顶部", id: "top" },
			],
			curSidebarId: "labs",
		}
	},
	mounted() {
		this.startNoticeContentLoop();

		this.labsTop = document.getElementById("labs").offsetTop;
		this.lessonsTop = document.getElementById("lessons").offsetTop;
		window.addEventListener("scroll", () => {
			this.onScroll();
		});
	},
	beforeDestroy() {
		if(this.noticeContentLoopInt){
			clearTimeout(this.noticeContentLoopInt);
		}
		window.removeEventListener(this.onScroll);
	},
	methods: {
		startNoticeContentLoop(idx = 0) {
			this.noticeContentLoopInt = setTimeout(() => {
				const i = idx + 1 > (noticeContentList.length - 1) ? 0 : (idx + 1);
				this.noticeContent = noticeContentList[i];

				this.startNoticeContentLoop(idx + 1);
			}, 5000);
		},

		alertMessage(text) {
			alert(text);
		},

		onScroll() {
			const scrollTop = document.documentElement.scrollTop;
			if(scrollTop >= this.labsTop){
				if(scrollTop >= this.lessonsTop){
					this.curSidebarId = "lessons";
				}else if(scrollTop >= this.labsTop){
					this.curSidebarId = "labs";
				}
			}else if(scrollTop >= 100){
				if(!this.sidebarVisible){
					this.sidebarVisible = true;
				}
			}else{
				this.sidebarVisible = false;
				this.curSidebarId = this.sidebarList[0].id;
			}
		},
		onHandleSideBar(id) {
			switch(id){
				case "top":
					window.scrollTo({
						top: 0,
						behavior: "smooth",
					});
					break;
				case "labs":
					this.curSidebarId = "labs";
					window.scrollTo({
						top: this.labsTop,
						behavior: "smooth",
					});
					break;
				case "lessons":
					this.curSidebarId = "lessons";
					window.scrollTo({
						top: this.lessonsTop,
						behavior: "smooth",
					});
					break;
			}
		}
	}
}
</script>

<style lang="less" scoped>
@import "@/common/theme.less";
.home{
	position: relative;
	min-width: @screen-min-width;
	color: @font-color;
	background-color: @divider-color;
	transition: all .2s linear;

	.notice{
		position: relative;
		display: flex;
		align-items: center;
		width: @screen-min-width;
		height: 70px;
		margin: 0 auto;
		padding: 0 28px;
		background-color: white;
		border-radius: 0 0 12px 12px;

		.icon-notice{
			width: 138px;
			height: 22px;
			background-image: url("https://coding.qq.com/home/dist/4cba4f0c88006ad6e6e9.png");
			background-position: 0px -40px;
		}
		.icon-hot{
			position: relative;
			width: 36px;
			border-radius: 8px 8px 8px 0;
			text-align: center;
			font-size: 12px;
			line-height: 16px;
			color: white;
			background-color: @tag-red-color;
		}
		.notice-content{
			margin: 0 10px 0 14px;
			cursor: pointer;

			&:hover{
				color: @primary-color;
			}
		}
	}

	.sidebar-fixed{
		position: fixed;
		z-index: 5;
		right: 20px;
		top: 50%;
		transform: translateY(50vh);
		opacity: 0;
		width: 60px;
		background-color: white;
		border-radius: 8px;
		box-shadow: 0px 0px 4px @box-shadow-color;
		overflow: hidden;
		transition: all .3s linear;

		&.visible{
			transform: translateY(-50%);
			opacity: 1;		
		}

		.sidebar-list{
			position: relative;
			width: 100%;

			.sidebar-item{
				position: relative;
				display: flex;
				flex-direction: column;
				justify-content: center;
				align-items: center;
				width: 100%;
				height: 68px;
				font-size: 12px;
				color: @font-color-gray;
				cursor: pointer;

				.sidebaricon{
					position: relative;
					font-size: 18px;
					margin-bottom: 6px;
				}

				&:not(:last-of-type){
					border-bottom: 1px solid @divider-color;
				}
				&:hover{
					background-color: @primary-color;
					color: white;
				}
				&.active{
					background-color: white;
					color: @primary-color;
				}
			}
		}
	}
}
</style>
