<template>
    <div>
        <div id="hand">
            <div v-for="(pai, idx) in noDrawingPai" :key="idx">
                <img :src="getTileSrc(pai)"/>
            </div>
            <img :src="getTileSrc(drawingPai)" v-if="drawingPai"/>
        </div>
        <div id="buttonArea">
            <button class="btn-border" @click="openTileSelector('m')">萬子</button>
            <button class="btn-border" @click="openTileSelector('s')">索子</button>
            <button class="btn-border" @click="openTileSelector('p')">筒子</button>
            <button class="btn-border" @click="openTileSelector('t')">字牌</button>
        </div>
        <tile-selector v-if="showTileSelector" @close="closeTileSelector">
            <div v-for="(pai, idx) in tiles[tileType]" :key="idx">
                <img :src="getTileSrc(pai)" class="paiSelector" @click="addPai(pai)"/>
            </div>
        </tile-selector>
        <div id="situation_box">
            <select v-model="situation.round">
                <option v-for="round in situation_conditions.round"
                        v-bind:value="round"
                        v-bind:key="round">
                    {{ round }}
                </option>
            </select>
            <label>場</label>
            <select v-model="situation.hand_number">
                <option v-for="hand_number in situation_conditions.hand_number"
                        v-bind:value="hand_number"
                        v-bind:key="hand_number">
                    {{ hand_number }}
                </option>
            </select>
            <label>局</label>
            <select v-model="situation.times">
                <option v-for="times in situation_conditions.times"
                        v-bind:value="times"
                        v-bind:key="times">
                    {{ times }}
                </option>
            </select>
            <label>本場</label>
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
    </div>
</template>

<script>
import TileSelector from '../components/TileSelector'

export default {
  name: 'register',
  components: {
      'tile-selector': TileSelector
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
          situation:  {
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
      tileSrc2: function(){
          const srcTemplate = './img/pai-images/'
          const tileSerial = ['1', '2', '3', '4', '5', '6', '7']
          const ext = '.png'

          let tileSrc = tileSerial.map(serial => srcTemplate + this.tileType + serial + ext)

          if(this.tileType !== 't'){
            //   tileSrc.splice(5, srcTemplate + this.tileType + '0' + ext) // 赤5
              tileSrc.push(srcTemplate + this.tileType + '8' + ext) // 8と9 字牌は7種なので
              tileSrc.push(srcTemplate + this.tileType + '9' + ext)
              tileSrc.push(srcTemplate + this.tileType + '0' + ext) // 赤5
          }
          console.log(tileSrc)
          return tileSrc
      },
      noDrawingPai: function(){
          if (this.hand.length < 14){
              return this.hand
          } else {
              return this.hand.slice(0, 13)
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
      getTileSrc: (pai) => {
          const srcTemplate = './img/pai-images/'
          return `${srcTemplate}${pai}.png`
      },
      addPai: function(pai){
          if (this.hand.length === 14){
              return
          }
          this.hand.push(pai)
      }
  }
}

</script>

<style scoped>
#hand {
    margin-left: 5%;
    width: 90%;
    height: 80px;
    border: solid;
    border-width: 1px;
    border-color: yellowgreen;
    border-color: #41b879;
    border-width: 2px;
    border-radius: 8px;
    display: flex;
}
#buttonArea {
    margin-top: 10px;
}
.btn-border{
    display: inline-block;
    margin: 3px;
    align-items: center;
    margin-top: 10px;
    margin-bottom: 15px;
}
#tiles {
    z-index: 2;
}
#tile_selector {
    z-index: 2;
    height: 40vh;
    width: 85vw;
    margin-left: 5%;
    margin-right: 10%;
    background-color: rgba( 20, 20, 20 );
    border: 4px solid gray;
    opacity: 0.20;
    position: fixed;
    display: block;
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