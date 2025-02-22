<template>
	<view style="background-color: #f4f4f4; min-height: 100vh;">
		<view class="status_bar"></view>
		<view>
			<view style="background-color: #FFFFFF;">
				<view class="row flex-row flex-space-between flex-align-center">
					<u--text text="名称(编号)" size="30"></u--text>
					<u--input border="surround" v-model="title" @change="changeA"></u--input>
				</view>
			</view>
			<view style="background-color: #FFFFFF;">
				<view class="row flex-row flex-space-between flex-align-center">
					<u--text text="速度" size="30"></u--text>
					<u--input placeholder="m/s" type="digit" border="surround" v-model="speed" @change="changeA"></u--input>
				</view>
			</view>
		</view>
		<view>
			<view class="title">井道顶部</view>
			<view style="background-color: #FFFFFF;">
				<view class="row flex-row flex-space-between flex-align-center">
					<u--text text="a.轿厢制导行程" size="30"></u--text>
					<u--input placeholder="m" type="digit" border="surround" v-model="guidanceInput" @change="changeA"></u--input>
					<view class="flex-10 flex-column">
						<text class="output-text ml-20">{{Number(guidanceOutput).toFixed(3)}}</text>
						<text class="output-text ml-20" :style="{color:(guidanceOutput > 0.1 ? 'green':'red')}">{{ guidanceOutput > 0.1 ? '合格': '不合格' }}</text>
					</view>
				</view>
			</view>
			<view style="background-color: #FFFFFF;">
				<view class="row flex-row flex-space-between flex-align-center">
					<u--text text="b.站人面" size="30"></u--text>
					<u--input placeholder="m" type="digit" border="surround" v-model="standAreaInput" @change="changeA"></u--input>
					<view class="flex-10 flex-column">
						<text class="output-text ml-20">{{Number(standAreaOutput).toFixed(3)}}</text>
						<text class="output-text ml-20" :style="{color:(standAreaOutput > 1 ? 'green':'red')}">{{ standAreaOutput > 1 ? '合格': '不合格' }}</text>
					</view>
				</view>
			</view>
			<view style="background-color: #FFFFFF;">
				<view class="row flex-row flex-space-between flex-align-center">
					<u--text text="c1.轿顶部件最高部分" size="28"></u--text>
					<u--input placeholder="m" type="digit" border="surround" v-model="topInput" @change="changeA"></u--input>
					<view class="flex-10 flex-column">
						<text class="output-text ml-20">{{Number(topOutput).toFixed(3)}}</text>
						<text class="output-text ml-20" :style="{color:(topOutput > 0.3 ? 'green':'red')}">{{ topOutput > 0.3 ? '合格': '不合格' }}</text>
					</view>
				</view>
			</view>
			<view style="background-color: #FFFFFF;">
				<view class="row flex-row flex-space-between flex-align-center">
					<u--text text="c2.导靴、悬挂端接附件" size="26"></u--text>
					<u--input placeholder="m" type="digit" border="surround" v-model="bottomInput" @change="changeA"></u--input>
					<view class="flex-10 flex-column">
						<text class="output-text ml-20">{{Number(bottomOutput).toFixed(3)}}</text>
						<text class="output-text ml-20" :style="{color:(bottomOutput > 0.1 ? 'green':'red')}">{{ bottomOutput > 0.1 ? '合格': '不合格' }}</text>
					</view>
				</view>
			</view>
			<view style="background-color: #FFFFFF;">
				<view class="row flex-row flex-space-between flex-align-center">
					<u--text text="对重缓冲器行程" size="30"></u--text>
					<u--input placeholder="m" type="digit" border="surround" v-model="cwBuffer" @change="changeA"></u--input>
				</view>
			</view>
			<view style="background-color: #FFFFFF;">
				<view class="row flex-row flex-space-between flex-align-center">
					<u--text text="对重最大越程距离" size="30"></u--text>
					<u--input placeholder="m" type="digit" border="surround" v-model="cwMaxDist" @change="changeA"></u--input>
				</view>
			</view>
			<view style="background-color: #FFFFFF;">
				<view class="row flex-row flex-space-between flex-align-center">
					<u--text text="e.对重制导行程" size="30"></u--text>
					<u--input placeholder="m" type="digit" border="surround" v-model="cwGuideRailDist" @change="changeA"></u--input>
					<view class="flex-10 flex-column">
						<text class="output-text ml-20">{{Number(cwGuideRailDist).toFixed(3)}}</text>
						<text class="output-text ml-20" :style="{color:(cwGuideRailDist > 0.1 ? 'green':'red')}">{{ cwGuideRailDist > 0.1 ? '合格': '不合格' }}</text>
					</view>
				</view>
			</view>
		</view>
		
		<view>
			<view class="title">井道底部</view>
			<view style="background-color: #FFFFFF;">
				<view class="row flex-row flex-space-between flex-align-center">
					<u--text text="f.底面与轿厢最低部件距离" size="22"></u--text>
					<u--input placeholder="m" type="digit" border="surround" v-model="carBottomToFloorDistInput" @change="changeA"></u--input>
					<view class="flex-10 flex-column">
						<text class="output-text ml-20">{{Number(carBottomToFloorDistOutput).toFixed(3)}}</text>
						<text class="output-text ml-20" :style="{color:(carBottomToFloorDistOutput > 0.5 ? 'green':'red')}">{{ carBottomToFloorDistOutput > 0.5 ? '合格': '不合格' }}</text>
					</view>
				</view>
			</view>
			<view style="background-color: #FFFFFF;">
				<view class="row flex-row flex-space-between flex-align-center">
					<u--text text="护脚板到墙" size="30"></u--text>
					<u--input placeholder="m" type="digit" border="surround" v-model="footGuardA" @change="changeA"></u--input>
				</view>
			</view>
			<view style="background-color: #FFFFFF;">
				<view class="row flex-row flex-space-between flex-align-center">
					<u--text text="g.护脚板到地" size="30"></u--text>
					<u--input placeholder="m" type="digit" border="surround" v-model="footGuardB" @change="changeA"></u--input>
					<view class="flex-10 flex-column">
						<text class="output-text ml-20">{{Number(footGuardOutput).toFixed(3)}}</text>
						<text class="output-text ml-20" :style="{color:(footGuardOutput > 0.5 ? 'green':'red')}">{{ footGuardOutput > 0.5 ? '合格': '不合格' }}</text>
					</view>
				</view>
			</view>
			<view style="background-color: #FFFFFF;">
				<view class="row flex-row flex-space-between flex-align-center">
					<u--text text="轿厢缓冲器行程" size="30"></u--text>
					<u--input placeholder="m" type="digit" border="surround" v-model="carBufferDist" @change="changeA"></u--input>
				</view>
			</view>
			<view style="background-color: #FFFFFF;">
				<view class="row flex-row flex-space-between flex-align-center">
					<u--text text="轿厢撞板与轿厢缓冲器顶面间的距离" size="20"></u--text>
					<u--input placeholder="m" type="digit" border="surround" v-model="carCollisionPlateToTopBufferDist" @change="changeA"></u--input>
				</view>
			</view>
		</view>
		
		<view>
			<view class="title">其他</view>
			<view style="background-color: #FFFFFF;">
				<view class="row flex-row flex-space-between flex-align-center">
					<u--text text="井道壁距离" size="30"></u--text>
					<u--input placeholder="m" type="digit" border="surround" v-model="wallDist" @change="changeA"></u--input>
				</view>
			</view>
			<view style="background-color: #FFFFFF;">
				<view class="row flex-row flex-space-between flex-align-center">
					<u--text text="对重(附件)到轿厢(附件)距离" size="26"></u--text>
					<u--input placeholder="m" type="digit" border="surround" v-model="cwToCarDist" @change="changeA"></u--input>
				</view>
			</view>
			<view style="background-color: #FFFFFF;">
				<view class="row flex-row flex-space-between flex-align-center">
					<u--text text="对重越程距离" size="30"></u--text>
					<u--input placeholder="m" type="digit" border="surround" v-model="cwOverrunDist" @change="changeA"></u--input>
				</view>
			</view>
		</view>
		<view class="flex-row" style="padding:20rpx;">
			<view>
				<u--text text="1、d轿顶上方有一个不小于0.50m×0.60m×0.80m的空间（任一平面朝下均可）" size="20"></u--text>
				<u--text text="2、h.高速电梯补偿绳反绳轮距离轿底最低部件" size="20"></u--text>
				<u--text text="3、i.底坑中有一个不小于0.50m×0.60m×1.00m的空间（任一平面朝下均可）" size="20"></u--text>
			</view>
			<u-button class="ml-20" style="flex-basis: 30%;" text="清空" type="primary" :plain="false" @click="show"></u-button>
		</view>
		<u-modal :show="showModal" title="清空" content="确认清空表单吗?" confirmText="确认" cancelText="取消" :showCancelButton="true" @confirm="clear" @cancel="cancel"></u-modal>
	</view>
</template>

<script>
	export default {
		
		data() {
			return {
				title: '',
				speed: null,
				guidanceInput: null,
				standAreaInput: null,
				topInput: null,
				bottomInput: null,
				cwBuffer: null,
				cwMaxDist: null,
				cwGuideRailDist: null,

				carBottomToFloorDistInput: null,
				footGuardA: null,
				footGuardB: null,
				carBufferDist: null,
				carCollisionPlateToTopBufferDist: null,

				wallDist: null,
				cwToCarDist: null,
				cwOverrunDist: null,

				showModal: false
			}
		},
		onLoad() {
			uni.getStorage({
				key: 'inputtings',
				success: (res) => {
					const cache = JSON.parse(res.data);
					this.title = cache.title;
					this.speed = cache.speed;
					this.guidanceInput = cache.guidanceInput;
					this.standAreaInput = cache.standAreaInput;
					this.topInput = cache.topInput;
					this.bottomInput = cache.bottomInput;
					this.cwBuffer = cache.cwBuffer;
					this.cwMaxDist = cache.cwMaxDist;
					this.cwGuideRailDist = cache.cwGuideRailDist;
								
					this.carBottomToFloorDistInput = cache.carBottomToFloorDistInput;
					this.footGuardA = cache.footGuardA;
					this.footGuardB = cache.footGuardB;
					this.carBufferDist = cache.carBufferDist;
					this.carCollisionPlateToTopBufferDist = cache.carCollisionPlateToTopBufferDist;
								
					this.wallDist = cache.wallDist;
					this.cwToCarDist = cache.cwToCarDist;
					this.cwOverrunDist = cache.cwOverrunDist;
				}
			});
			
		},
		computed: {
			guidanceOutput: function() {
				return this.guidanceInput - this.cwBuffer - this.cwMaxDist - (this.speed * this.speed * 0.035);
			},
			standAreaOutput: function() {
				return this.standAreaInput - this.cwBuffer - this.cwMaxDist - (this.speed * this.speed * 0.035);
			},
			topOutput: function() {
				return this.topInput - this.cwBuffer - this.cwMaxDist - (this.speed * this.speed * 0.035);
			},
			bottomOutput: function() {
				return this.bottomInput - this.cwBuffer - this.cwMaxDist - (this.speed * this.speed * 0.035);
			},
			carBottomToFloorDistOutput: function() {
				return this.carBottomToFloorDistInput - this.carBufferDist - this.carCollisionPlateToTopBufferDist;
			},
			footGuardOutput: function() {
				return this.footGuardB - this.carBufferDist - this.carCollisionPlateToTopBufferDist;
			}
		},
		methods: {
			changeA() {
				const stringifyData = JSON.stringify({
					title: this.title,
					speed: this.speed,
					guidanceInput: this.guidanceInput,
					standAreaInput: this.standAreaInput,
					topInput: this.topInput,
					bottomInput: this.bottomInput,
					cwBuffer: this.cwBuffer,
					cwMaxDist: this.cwMaxDist,
					cwGuideRailDist: this.cwGuideRailDist,

					carBottomToFloorDistInput: this.carBottomToFloorDistInput,
					footGuardA: this.footGuardA,
					footGuardB: this.footGuardB,
					carBufferDist: this.carBufferDist,
					carCollisionPlateToTopBufferDist: this.carCollisionPlateToTopBufferDist,

					wallDist: this.wallDist,
					cwToCarDist: this.cwToCarDist,
					cwOverrunDist: this.cwOverrunDist,
				})
				uni.setStorage({
					key: 'inputtings',
					data: stringifyData
				});
			},
			show() {
				this.showModal = true;
			},
			cancel() {
				this.showModal = false;
			},
			clear() {
				this.title = '';
				this.speed = null;
				this.guidanceInput = null;
				this.standAreaInput = null;
				this.topInput = null;
				this.bottomInput = null;
				this.cwBuffer = null;
				this.cwMaxDist = null;
				this.cwGuideRailDist = null;
			
				this.carBottomToFloorDistInput = null;
				this.footGuardA = null;
				this.footGuardB = null;
				this.carBufferDist = null;
				this.carCollisionPlateToTopBufferDist = null;
			
				this.wallDist = null;
				this.cwToCarDist = null;
				this.cwOverrunDist = null;
				
				this.showModal = false;
			}
		}
	}
</script>

<style lang="scss">
	/* 注意要写在第一行，同时给style标签加入lang="scss"属性 */
	@import "uview-ui/index.scss";

	.title {
		padding: 10rpx;
	}
	
	.flex-10 { flex-basis: 13%; overflow: hidden; }
	.row { padding: 4rpx 20rpx;}
	.output-text { font-size: 18rpx; }
	.margin-left { margin-left: auto; }
	.status_bar {
		height: var(--status-bar-height);
		width: 100%;
	}
</style>
