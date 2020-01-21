<template>
  <v-ons-page>
    <div class="gradation">
      <h1 align="center" style="color:white;margin-top:-20px">SmartPoker</h1>
      <g fill="none" fill-rule="nonzero" stroke="none" stroke-width="1" stroke-linecap="butt" stroke-linejoin="miter" stroke-miterlimit="10" stroke-dasharray="" stroke-dashoffset="0" font-family="none" font-weight="none" font-size="none" text-anchor="none" style="mix-blend-mode: normal"><path d="M0,172v-172h172v172z" fill="none"></path><g fill="#eeeeee"><path d="M143.19336,21.43001c-0.26705,0.00844 -0.53341,0.03181 -0.79785,0.06999h-34.89551c-2.58456,-0.03655 -4.98858,1.32136 -6.29153,3.55376c-1.30295,2.2324 -1.30295,4.99342 0,7.22582c1.30295,2.2324 3.70697,3.59031 6.29153,3.55376h18.53256l-66.59961,66.59961c-1.8722,1.79752 -2.62637,4.46674 -1.97164,6.97823c0.65473,2.51149 2.61604,4.4728 5.12753,5.12753c2.51149,0.65473 5.18071,-0.09944 6.97823,-1.97165l66.59961,-66.59961v18.53255c-0.03655,2.58456 1.32136,4.98858 3.55376,6.29153c2.2324,1.30295 4.99342,1.30295 7.22582,0c2.2324,-1.30295 3.59031,-3.70697 3.55376,-6.29153v-34.9235c0.28889,-2.08845 -0.35639,-4.19816 -1.76411,-5.76769c-1.40772,-1.56953 -3.43507,-2.43964 -5.54253,-2.3788zM35.83333,21.5c-7.83362,0 -14.33333,6.49972 -14.33333,14.33333v100.33333c0,7.83362 6.49972,14.33333 14.33333,14.33333h100.33333c7.83362,0 14.33333,-6.49972 14.33333,-14.33333v-43c0.03655,-2.58456 -1.32136,-4.98858 -3.55376,-6.29153c-2.2324,-1.30295 -4.99342,-1.30295 -7.22582,0c-2.2324,1.30295 -3.59031,3.70697 -3.55376,6.29153v43h-100.33333v-100.33333h43c2.58456,0.03655 4.98858,-1.32136 6.29153,-3.55376c1.30295,-2.2324 1.30295,-4.99342 0,-7.22582c-1.30295,-2.2324 -3.70697,-3.59031 -6.29153,-3.55376z"></path></g></g>
      <v-ons-card style="margin-top:-20px">
        <div class="flex_box2">
          <div class="imgtable-content">
            <img class="i" src="./images/pokertable2.png">
          <div v-for="(item,i) of players" v-bind:key="item.name">
            <div style="background-color: rgba(0,0,0,0.8);color:white;padding:8px" v-bind:class="tableplayer[i]" v-bind:style="[players[i].name === turn? tableLightup:''] " v-bind:key="item.name">
                PLAYER{{i+1}}<br><b>{{ item.name }}</b>
              </div>
            </div>
          </div>
        </div>
        <form @submit.prevent="submit">
          <div align="center" style="margin-top:5%;"><v-ons-button type="submit" @click="submit()">ゲームスタート</v-ons-button></div>
        </form>
      </v-ons-card>
    </div>
  </v-ons-page>
</template>

<script>
import page1 from "./page1.vue";
import page2 from "./page2.vue";

export default {
  data() {
    return {
      player: this.$store.state.player,
      chip: this.$store.state.chip,
      players: [],
      flash:[],
      tableplayer:[],
      tableLightup:{
      backgroundColor: "#d4f0fd",
      }
    };
  },
  watch: {
  },
  created() {
    //プレイヤー設定
    for (let i = 0; i < this.player.length; i++) {
      let addPlayer = {
        name: this.player[i],
        chip: this.chip,
        bet: 0,
        isplay: 0
      };
      this.players.push(addPlayer);
      this.flash.push(false);
    }
    //席順
    for (let i = this.players.length - 1; i >= 0; i--) {
      let rand = Math.floor(Math.random() * (i + 1));
      [this.players[i], this.players[rand]] = [
        this.players[rand],
        this.players[i]
      ];
    }

    ///テーブル配置
    switch( this.players.length ) {
      case 1:
          this.tableplayer[0] = "table-player8";
          break;
      case 2:
          this.tableplayer[0] = "table-player8";
          this.tableplayer[1] = "table-player9";
          break;
      case 3:
          this.tableplayer[0] = "table-player8";
          this.tableplayer[1] = "table-player6";
          this.tableplayer[2] = "table-player4";
          break;
      case 4:
          this.tableplayer[0] = "table-player2";
          this.tableplayer[1] = "table-player3";
          this.tableplayer[2] = "table-player1";
          this.tableplayer[3] = "table-player0";
          break;
      case 5:
          this.tableplayer[0] = "table-player8";
          this.tableplayer[1] = "table-player5";
          this.tableplayer[2] = "table-player6";
          this.tableplayer[3] = "table-player4";
          this.tableplayer[4] = "table-player7";
          break;
      case 6:
          this.tableplayer[0] = "table-player8";
          this.tableplayer[1] = "table-player5";
          this.tableplayer[2] = "table-player6";
          this.tableplayer[3] = "table-player9";
          this.tableplayer[4] = "table-player4";
          this.tableplayer[5] = "table-player7";
          break;
      case 7:
          this.tableplayer[0] = "table-player8";
          this.tableplayer[1] = "table-player5";
          this.tableplayer[2] = "table-player6";
          this.tableplayer[3] = "table-player1";
          this.tableplayer[4] = "table-player0";
          this.tableplayer[5] = "table-player4";
          this.tableplayer[6] = "table-player7";
          break;
      case 8:
          this.tableplayer[0] = "table-player3";
          this.tableplayer[1] = "table-player5";
          this.tableplayer[2] = "table-player6";
          this.tableplayer[3] = "table-player1";
          this.tableplayer[4] = "table-player0";
          this.tableplayer[5] = "table-player4";
          this.tableplayer[6] = "table-player7";
          this.tableplayer[7] = "table-player2";
          break;

      default:
      break;
    }
  },
  computed: {
    bet0: function() {
      flash[0].push(true);
    },
    bet1: function() {
      flash[1].push(true);
    },
    bet2: function() {
      flash[2].push(true);
    },
    bet3: function() {
      flash[3].push(true);
    }
  },
  methods: {
    submit: function(){
      this.$store.state.players = this.players;
      this.$store.commit("navigator/push", page2);
    },
  }
};
</script>


<style scoped>
@import url(https://cdnjs.cloudflare.com/ajax/libs/animate.css/3.7.2/animate.min.css);
.gradation{
    margin-top: -60px;
    padding-top: 7%;
    width: 100%;
    height: 135%;
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
.pod{
  vertical-align: middle;
}
.bet{
  vertical-align: middle;
}
.flex_box{
  display: flex;

}

 i{
  position: relative;
  left: 0;
  right: 0;
  margin: auto;
}


.text_content{
  /* margin-left:10px; */
 padding-left:5%;
}
.table_content{
  /* margin-right: 10px; */
  padding-right:20%;
  width: 200%;
}

table {
  border-collapse: collapse;
  border-spacing: 0;
  table-layout: auto;
}

table tr {
  border-bottom: solid 1px #eee;
  cursor: pointer;
}

table th,
table td {
  text-align: center;
  width: 25%;
  padding: 15px 0;
}

/* テーブル画像について */
.flex_box2 {
  display: flex;
  /* flex-direction: column; */
  justify-content: center;

  padding-top: 36px;
}
.imgtable-content {
  position: relative;
}
.table-text-center{
  position: absolute;
  top: 32%;
  left: 35%;
  padding: 10px;
  color:white;
  background-color: rgba(255,255,255,0)
}
.table-text-player{
  background-color:rgba(0,0,0,0.6)
}
.table-player0{
  position: absolute;
  top: 76%;
  left: 35%;
  background-color:rgba(0,0,0,0.6);
  border:solid;
  font-size:24px;
}
.table-player1{
  position: absolute;
  top: 76%;
  left: 56%;
  border:solid;
  background-color:rgba(0,0,0,0.6);
  font-size:24px;
}
.table-player2{
  position: absolute;
  top: 3%;
  left: 35%;
  border:solid;
  background-color:rgba(0,0,0,0.6);
  font-size:24px;
}
.table-player3{
  position: absolute;
  top: 3%;
  left: 56%;
  border:solid;
  background-color:rgba(0,0,0,0.6);
  font-size:24px;
}
.table-player4{
  position: absolute;
  top: 60%;
  left: 17%;
  border:solid;
  background-color:rgba(0,0,0,0.6);
  font-size:24px;
}
.table-player5{
  position: absolute;
  top: 22%;
  left: 74%;
  border:solid;
  background-color:rgba(0,0,0,0.6);
  font-size:24px;
}
.table-player6{
  position: absolute;
  top: 60%;
  left: 74%;
  border:solid;
  background-color:rgba(0,0,0,0.6);
  font-size:24px;
}
.table-player7{
  position: absolute;
  top: 22%;
  left: 17%;
  border:solid;
  background-color:rgba(0,0,0,0.6);
  font-size:24px;
}
.table-player8{
  position: absolute;
  top: 3%;
  left:46%;
  border:solid;
  background-color:rgba(0,0,0,0.6);
  font-size:24px;
}
.table-player9{
  position: absolute;
  top: 76%;
  left:46%;
  border:solid;
  background-color:rgba(0,0,0,0.6);
  font-size:24px;
}
</style>
