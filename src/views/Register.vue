<template>
    <div>
        <div id="hand">
            <img v-for="tile in hand" v-bind:key="tile" v-bind:src="tile_img['tile']">
        </div>
        <div id="buttonArea">
            <button class="btn-border">萬子</button>
            <button class="btn-border">索子</button>
            <button class="btn-border">筒子</button>
            <button class="btn-border">字牌</button>
            <div id="tiles">
            </div>
        </div>
        <div>
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
        <div>
            <label class="point_label">持ち点</label>
            <input v-bind="points.self"/>
        </div>
        <div>
            <label class="point_label">下家</label>
            <input v-bind="points.right"/>
        </div>
        <div>
            <label class="point_label">対面</label>
            <input v-bind="points.opposite"/>
        </div>
        <div>
            <label class="point_label">上家</label>
            <input v-bind="points.left"/>
        </div>
        <label>メモ</label>
        <textarea v-model="note"></textarea>
    </div>
</template>

<script>

export default {
  name: 'register',
  data(){
      return {
          hand: [],
          tile: {

          },
          tile_img: {

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
}
#buttonArea {
    margin-top: 10px;
}
.btn-border{
    margin: 3px;
}
#tiles {
    z-index: 2;
}
.point_label{
    width: 0.5rem;
}
</style>