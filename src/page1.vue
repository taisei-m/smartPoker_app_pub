<template id="setting">
<v-ons-page >
   <div class="gradation" style="padding-top:5%;">
    <g fill="none" fill-rule="nonzero" stroke="none" stroke-width="1" stroke-linecap="butt" stroke-linejoin="miter" stroke-miterlimit="10" stroke-dasharray="" stroke-dashoffset="0" font-family="none" font-weight="none" font-size="none" text-anchor="none" style="mix-blend-mode: normal"><path d="M0,172v-172h172v172z" fill="none"></path><g fill="#eeeeee"><path d="M143.19336,21.43001c-0.26705,0.00844 -0.53341,0.03181 -0.79785,0.06999h-34.89551c-2.58456,-0.03655 -4.98858,1.32136 -6.29153,3.55376c-1.30295,2.2324 -1.30295,4.99342 0,7.22582c1.30295,2.2324 3.70697,3.59031 6.29153,3.55376h18.53256l-66.59961,66.59961c-1.8722,1.79752 -2.62637,4.46674 -1.97164,6.97823c0.65473,2.51149 2.61604,4.4728 5.12753,5.12753c2.51149,0.65473 5.18071,-0.09944 6.97823,-1.97165l66.59961,-66.59961v18.53255c-0.03655,2.58456 1.32136,4.98858 3.55376,6.29153c2.2324,1.30295 4.99342,1.30295 7.22582,0c2.2324,-1.30295 3.59031,-3.70697 3.55376,-6.29153v-34.9235c0.28889,-2.08845 -0.35639,-4.19816 -1.76411,-5.76769c-1.40772,-1.56953 -3.43507,-2.43964 -5.54253,-2.3788zM35.83333,21.5c-7.83362,0 -14.33333,6.49972 -14.33333,14.33333v100.33333c0,7.83362 6.49972,14.33333 14.33333,14.33333h100.33333c7.83362,0 14.33333,-6.49972 14.33333,-14.33333v-43c0.03655,-2.58456 -1.32136,-4.98858 -3.55376,-6.29153c-2.2324,-1.30295 -4.99342,-1.30295 -7.22582,0c-2.2324,1.30295 -3.59031,3.70697 -3.55376,6.29153v43h-100.33333v-100.33333h43c2.58456,0.03655 4.98858,-1.32136 6.29153,-3.55376c1.30295,-2.2324 1.30295,-4.99342 0,-7.22582c-1.30295,-2.2324 -3.70697,-3.59031 -6.29153,-3.55376z"></path></g></g>
  <v-ons-card>
  <div  align=center>
  <h1>Smart Poker</h1>
  <h2>グループID:{{groupID}}</h2>
  <div>
    <h2>ゲーム設定</h2>
    <form @submit.prevent="submit">
      <label>プレイヤー</label>
      <label><input  type="checkbox" :checked="isAllSelected" @click="selectAll" >ALL</label>
      <div v-for="(name, i) in names" :key="i" >
        <input :id="'name' + i" type="checkbox" :value="name" v-model="player">
        <label :for="'player' + i">{{name}}</label>
    </div><br>
      <div><label for="maxRound">ラウンド</label><br>
      <input type="number" v-model="maxRound"></div><br>
      <div><label for="chip">チップ</label><br>
      <input type="number" v-model="chip"></div><br>
      <div><label for="minbet">最低ベット</label><br>
      <input type="number" v-model="minBet"></div><br>
      <div><v-ons-button type="submit" @click="submit()">ゲームスタート</v-ons-button></div>
    </form>
  </div>
  </div>
  </v-ons-card>
  </div>
  </v-ons-page>
</template>

<script>
import page2 from './page2.vue'
import page3 from './page3.vue'

export default {
  data() {
    return {
      groupID:null,
      names: [],
      player: [],
      maxRound: 4,
      chip: 300,
      minBet: 10,
      players: [],
      isAllSelected: false,
      record:{},
    };
  },
  created(){
    this.fetch();
  },
  watch:{
  },
  methods: {
    submit: function(){
      this.$store.state.player = this.player;
      this.$store.state.maxRound = Number(this.maxRound);
      this.$store.state.chip = Number(this.chip);
      this.$store.state.minBet = Number(this.minBet);
      this.$store.commit("navigator/push", page2);
    },
    selectAll () {
      if (this.isAllSelected) {
        this.player = []
        this.isAllSelected = false
      } else {
        this.player = []
        for (var name in this.names) {
          this.player.push(this.names[name])
        }
        this.isAllSelected = true
      }
    },
    fetch(){
      fetch(this.$url + "/record"+"?recordID="+localStorage.getItem("recordID"), {method: 'GET'})
  .then((res) => {
    // 返されたBodyをjsonにしてPromise.resolve()する
    return res.json();
  })
  .then((data) => {
    // api_url から返されたデータ(json)
    // 実際にデータを加工したり色々する
    for (let i = 0; i < 8; i++) {
      let j =eval("data.record.name"+i+".value");
      if( j != "null" && j !=""){
      let addPlayer = j;
      this.names.push(addPlayer);
      }
    }
    this.selectAll();
    this.groupID = data.record.groupId.value;
    this.maxRound = this.player.length;
  })
  .catch((err) => {
    console.error( err );
  });
    }
  }
};
</script>
<style scoped>
.gradation{
    margin-top: -60px;
    width: 100%;
    height: 115%;
    font-family: "Exo", sans-serif;
    color: black;
    background: linear-gradient(-45deg, #ee7752, #e73c7e, #23a6d5, #23d5ab);
    background-size: 400% 400%;
    animation: gradientBG 15s ease infinite;

}


@keyframes gradientBG {
    0% {
        background-position: 0% 50%;
    }
    50% {
        background-position: 100% 50%;
    }
    100% {
        background-position: 0% 50%;
    }
}
</style>
