<template>
	<div class="main-box">
		<div id="hand">
			<div v-for="(pai, idx) in noDrawingPai" :key="idx">
				<img :src="getTileSrc(pai, 'hand')"/>
			</div>
			<div>
				<img :src="getTileSrc(drawingPai, 'hand')" v-if="drawingPai" id="justDrawing"/>
			</div>
		</div>
		<div class="horizontal-flex">
			<floating-button @click="openTileSelector('m')">萬子</floating-button>
			<floating-button @click="openTileSelector('s')">索子</floating-button>
			<floating-button @click="openTileSelector('p')">筒子</floating-button>
			<floating-button @click="openTileSelector('t')">字牌</floating-button>
			<floating-button @click="clearHand()">クリア</floating-button>
		</div>
		<tile-selector v-if="showTileSelector" @close="closeTileSelector">
			<div v-for="(pai, idx) in tiles[tileType]" :key="idx">
				<img :src="getTileSrc(pai, 'selector')" class="paiSelector" @click="addPai(pai)"/>
			</div>
		</tile-selector>
		<div class="horizontal-flex">
			<selector-whit-unit
				unit="場"
				:candidates="situation_conditions.round"
				v-model="situation.round">
			</selector-whit-unit>
			<selector-whit-unit
				unit="局"
				:candidates="situation_conditions.hand_number"
				v-model="situation.hand_number">
			</selector-whit-unit>
			<selector-whit-unit
				unit="本場"
				:candidates="situation_conditions.times"
				v-model="situation.times">
			</selector-whit-unit>
		</div>
		<div class="point_box">
			<label>持ち点</label>
			<input v-bind="points.self" type="number"/>
		</div>
		<div class="point_box">
			<label>下家</label>
			<input v-bind="points.right" type="number"/>
		</div>
		<div class="point_box">
			<label>対面</label>
			<input v-bind="points.opposite" type="number"/>
		</div>
		<div class="point_box">
			<label>上家</label>
			<input v-bind="points.left" type="number"/>
		</div>
		<label>メモ</label>
		<textarea v-model="note"></textarea>
		<floating-button @click="clearHand()">登録</floating-button>
	</div>
</template>

<script>
import TileSelector from '../components/TileSelector'
import FloatingButton from '../components/FloatingButton'
import SelectorWithUnit from '../components/SelectorWithUnit'

export default {
	name: 'register',
	components: {
		'tile-selector': TileSelector,
		'floating-button': FloatingButton,
		'selector-whit-unit': SelectorWithUnit
	},
	data(){
		return {
			hand: [],
			showTileSelector: false,
			tileType: "m",
			tiles: {
				'm': ['m1', 'm2', 'm3', 'm4', 'm5', 'm6', 'm7', 'm8', 'm9', 'm0'],
				's': ['s1', 's2', 's3', 's4', 's5', 's6', 's7', 's8', 's9', 's0'],
				'p': ['p1', 'p2', 'p3', 'p4', 'p5', 'p6', 'p7', 'p8', 'p9', 'p0'],
				't': ['t1', 't2', 't3', 't4', 't5', 't6', 't7']
			},
			situation:	{
				round: '東', // 場風
				hand_number: 1, // 局数
				times: 0 // n本場 英語の正式名称が知りたい
			},
			situation_conditions: { // リストボックス選択肢
				round: ['東', '南', '西', '北'],
				hand_number: [1, 2, 3, 4],
				times: [0, 1, 2, 3, 4, 5, 6, 7, 8]
			},
			points: {
				self: null,
				right: null,
				opposite: null,
				left: null
			},
			note: ""
		}
	},
	computed: {
		noDrawingPai: function(){
			if (this.hand.length < 14){
				return this.hand
			} else {
				return this.hand.slice(0, 12)
			}
		},
		drawingPai: function(){
			if (this.hand.length < 14){
				return ""
			} else {
				return this.hand[13]
			}
		}
	},
	methods: {
		openTileSelector: function(tileType){
			this.tileType = tileType
			this.showTileSelector = true
		},
		closeTileSelector: function(){
			this.showTileSelector = false
		},
		getTileSrc: (pai, type) => {
			const isSelector = type =='selector' ? true : false
			const srcTemplate = isSelector ? './img/pai-images/for_selector/' : './img/pai-images/for_hand/'
			const extension = isSelector ? '.png' : '.jpg'
			return `${srcTemplate}${pai}${extension}`
		},
		addPai: function(pai){
			if (this.hand.length === 14){
				return
			}
			this.hand.push(pai)
		},
		clearHand: function(){
			this.hand = []
		},
		regist: function(){
			
		}
	}
}

</script>

<style scoped>
	#hand {
		margin-left: 5%;
		width: 90%;
		height: 70px;
		border: solid;
		border-width: 1px;
		border-color: #41b879;
		border-width: 2px;
		border-radius: 8px;
		display: flex;
		justify-content: center;
		align-items: center;
	}
	#justDrawing{
		padding-left: 10px;
	}
	#buttonArea {
		margin-top: 10px;
	}
	.paiSelector {
		margin: 10px;
	}
	#situation_box {
		display: flex;
		justify-content: space-around;
		align-items: center;
	}
	.point_label {
		width: 0.5rem;
	}
	.point_box {
		display: flex;
		justify-content: center;
		align-items: center;
		padding: 3px;
	}
	.point_box input{
		margin: 5px;
		width: 40%
		
	}
	.point_box label{
		display: block;
		width: 20%;
		text-align: center;
	}
</style>