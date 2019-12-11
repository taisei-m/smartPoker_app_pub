<template>
  <v-ons-page>
    <div class="gradation">
    <g fill="none" fill-rule="nonzero" stroke="none" stroke-width="1" stroke-linecap="butt" stroke-linejoin="miter" stroke-miterlimit="10" stroke-dasharray="" stroke-dashoffset="0" font-family="none" font-weight="none" font-size="none" text-anchor="none" style="mix-blend-mode: normal"><path d="M0,172v-172h172v172z" fill="none"></path><g fill="#eeeeee"><path d="M143.19336,21.43001c-0.26705,0.00844 -0.53341,0.03181 -0.79785,0.06999h-34.89551c-2.58456,-0.03655 -4.98858,1.32136 -6.29153,3.55376c-1.30295,2.2324 -1.30295,4.99342 0,7.22582c1.30295,2.2324 3.70697,3.59031 6.29153,3.55376h18.53256l-66.59961,66.59961c-1.8722,1.79752 -2.62637,4.46674 -1.97164,6.97823c0.65473,2.51149 2.61604,4.4728 5.12753,5.12753c2.51149,0.65473 5.18071,-0.09944 6.97823,-1.97165l66.59961,-66.59961v18.53255c-0.03655,2.58456 1.32136,4.98858 3.55376,6.29153c2.2324,1.30295 4.99342,1.30295 7.22582,0c2.2324,-1.30295 3.59031,-3.70697 3.55376,-6.29153v-34.9235c0.28889,-2.08845 -0.35639,-4.19816 -1.76411,-5.76769c-1.40772,-1.56953 -3.43507,-2.43964 -5.54253,-2.3788zM35.83333,21.5c-7.83362,0 -14.33333,6.49972 -14.33333,14.33333v100.33333c0,7.83362 6.49972,14.33333 14.33333,14.33333h100.33333c7.83362,0 14.33333,-6.49972 14.33333,-14.33333v-43c0.03655,-2.58456 -1.32136,-4.98858 -3.55376,-6.29153c-2.2324,-1.30295 -4.99342,-1.30295 -7.22582,0c-2.2324,1.30295 -3.59031,3.70697 -3.55376,6.29153v43h-100.33333v-100.33333h43c2.58456,0.03655 4.98858,-1.32136 6.29153,-3.55376c1.30295,-2.2324 1.30295,-4.99342 0,-7.22582c-1.30295,-2.2324 -3.70697,-3.59031 -6.29153,-3.55376z"></path></g></g>
<!-- master kkk-->
<!-- gjsdkfjsdfjsfjklfjsdf;fjsdl -->
    <v-ons-card>
        <h1 class="animated pulse slow" style="text-align: center; padding-top: 20px">Smart Poker　　ラウンド：{{round}}/{{maxRound}}</h1>
      <div class="flex_box1">
        <div>
          <br />
          <br />
          <div class="table_content">
            <table border="2">
            <tr><th>role</th><th>Player</th><th>Chip</th><th>Bet</th></tr>
            <tr v-for="(item,i) of players" v-bind:key="item.name" v-bind:class="{active: item.name==turn,isfold: item.isplay==1}">
              <!-- <td></td><td>PLAYER{{i+1}}<br>{{ item.name }}</td><td>{{ item.chip }}</td><td v-bind:class="['emphasize'+i]">{{ item.bet }}</td> -->
              <td></td><td>PLAYER{{i+1}}<br>{{ item.name }}</td><td>{{ item.chip }}</td><td v-bind:class="{'animated flash slow': flash[i]}">{{ item.bet }}</td>
            </tr>
            </table>
          </div>
        </div>

        <div class="flex_box2">


        <div class="text_content">
            <table border="2" style="width: 700px"  >
           <tr>
            <th v-bind:class="{preflop: br==0}">プリフロップ</th>
            <th v-bind:class="{flop: br==1}">フロップ</th>
            <th v-bind:class="{turnCL: br==2}">ターン</th>
            <th v-bind:class="{river: br==3}">リバー</th>
           </tr>
          </table>
        </div>
        <div class="imgtable-content">
          <img src="./images/tableimage700.jpg">
          <div class="table-text-center">
            <h1><img src="./images/tips_original.jpg" width="40px" height="30px" class="pod">ポット:{{pot}}</h1>
            <h2><img src="./images/tip_original.jpg" width="40px" height="30px" class="bet">ベット:{{pay}}</h2>
          </div>
          <!-- <div class="table-text-player"> -->
            <!-- <div v-for="(item,i) of players" v-bind:key="item.name" v-bind:class="{isfold: item.isplay==1}" align="center"> -->
            <!-- </div> -->
            <div v-for="(item,i) of players" v-bind:key="item.name">
              <!-- <td></td><td>PLAYER{{i+1}}<br>{{ item.name }}</td><td>{{ item.chip }}</td><td v-bind:class="['emphasize'+i]">{{ item.bet }}</td> -->
              <!-- <div v-bind:class="['table-player'+i]"> -->
              <div v-bind:class="tableplayer[i]" v-bind:style="[players[i].name === turn? tableLightup:''] " v-bind:key="item.name">
                <div v-if="players[i].name === turn" style="backgroundColor:yellow">☆Your Turn☆</div>
                PLAYER{{i+1}}<br>{{ item.name }}<br>Chip：{{ item.chip }}
              </div>
            </div>

          <!-- </div> -->
        </div>
      </div>
      </div>

      <br />
      <modal name="winner-modal" width="60%"  height="80%">
        <div align="center">
          <h2>ショーダウン</h2>
          ラウンド{{round}}終了です。
          勝利プレイヤーを「プレイヤー'番号'」で言ってください。
          <table border="2">
            <tr v-for="(item,i) of players" v-bind:key="item.name" v-bind:class="{isfold: item.isplay==1}" align="center">
              <td>PLAYER{{i+1}}</td><td>{{ item.name }}</td>
            </tr>
            </table>
        </div>
      </modal>

      <modal name="action-modal" width="50%"  height="20%">
        <div align="center" style="line-height:100px;">
          <h1>{{action}}</h1>
        </div>
      </modal>
      <modal name="err-modal" width="50%"  height="20%">
        <div align="center" style="line-height:100px; color:red;">
          <h1>{{comment}}</h1>
        </div>
      </modal>
    </v-ons-card>
    </div>
  </v-ons-page>
</template>

<script>
import page1 from "./page1.vue";
import page3 from "./page3.vue";

export default {
  data() {
    return {
      player: this.$store.state.player,
      maxRound: this.$store.state.maxRound,
      chip: this.$store.state.chip,
      minBet: this.$store.state.minBet,
      array: [],
      round: 1,
      dealer: "",
      pot: 0,
      bettingRound: ["プリフロップ", "フロップ", "ターン", "リバー"],
      br: 3,
      players: [],
      allBet: 0,
      order: "",
      turn: "",
      action: "",
      p: 0,
      selectActionValue: "",
      selectActionOptions: {
        1: "ベット",
        2: "コール",
        3: "レイズ",
        4: "チェック",
        5: "フォールド",
        6: "オールイン"
      },
      selectWinnerValue: "",
      update: null,
      pay: 10,
      playing: 0,
      comment: "",
      winComment: "",
      checkCount: 0,
      record: [],
      timer: null,
      w: 0,
      win: 9,
      wc: 0,

      flash: [true, true, true, false, false, false],
      tableplayer:[],
      tableLightup:{
      backgroundColor: "red",
      }
    };
  },
  watch: {
    update: function() {
      this.w++;
      if (this.w != 1 && this.wc == 0) {
        console.log("update");
        this.submit();
      } else if (this.wc == 1) {
        console.log("winner");
        this.winner();
      }
    },
    win: function() {
      if (this.win != "" || this.win == 0) {
        console.log("winner");
        this.winner();
      }
    }
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
    }
    //席順
    for (let i = this.players.length - 1; i >= 0; i--) {
      let rand = Math.floor(Math.random() * (i + 1));
      [this.players[i], this.players[rand]] = [
        this.players[rand],
        this.players[i]
      ];
    }
    //席順のコンソール出力
    let q = 0;
    for (let item in this.players) {
      this.order = this.order + this.players[item]["name"] + ",";
      q++;
      if (q == this.players.length) {
        console.log(this.order + "の順です。");
      }
    }
    console.log("ラウンド:" + this.round);
    //プリフロップ
    console.log(this.bettingRound[0]);
    //ディーラーを決定
    this.dealer = this.players[0].name;
    console.log("ディーラー:" + this.dealer);
    this.playing = this.players.length;
    this.sbbb();




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
        this.tableplayer[1] = "table-player4";
        this.tableplayer[2] = "table-player6";
        break;
    case 4:
        this.tableplayer[0] = "table-player2";
        this.tableplayer[1] = "table-player0";
        this.tableplayer[2] = "table-player1";
        this.tableplayer[3] = "table-player3";
        break;
    case 5:
        this.tableplayer[0] = "table-player8";
        this.tableplayer[1] = "table-player7";
        this.tableplayer[2] = "table-player4";
        this.tableplayer[3] = "table-player6";
        this.tableplayer[4] = "table-player5";
        break;
    case 6:
        this.tableplayer[0] = "table-player8";
        this.tableplayer[1] = "table-player7";
        this.tableplayer[2] = "table-player4";
        this.tableplayer[3] = "table-player9";
        this.tableplayer[4] = "table-player6";
        this.tableplayer[5] = "table-player5";
        break;
    case 7:
        this.tableplayer[0] = "table-player8";
        this.tableplayer[1] = "table-player7";
        this.tableplayer[2] = "table-player4";
        this.tableplayer[3] = "table-player0";
        this.tableplayer[4] = "table-player1";
        this.tableplayer[5] = "table-player6";
        this.tableplayer[6] = "table-player5";
        break;
    case 8:
        this.tableplayer[0] = "table-player2";
        this.tableplayer[1] = "table-player7";
        this.tableplayer[2] = "table-player4";
        this.tableplayer[3] = "table-player0";
        this.tableplayer[4] = "table-player1";
        this.tableplayer[5] = "table-player6";
        this.tableplayer[6] = "table-player5";
        this.tableplayer[7] = "table-player3";
        break;

    default:
        break;
}




    ////数字強調
    this.bet0 = players[0].bet;
    this.bet1 = players[1].bet;
    this.bet2 = players[2].bet;
    this.bet3 = players[3].bet;




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
    submit: function() {
      console.log("submit");
      //this.action = this.selectActionValue;//commentin
      //console.log(this.selectActionValue);//commentin
      console.log(this.action);
      this.winComment = "";
      //this.action = this.selectActionOptions[this.selectActionValue];
      if (
        this.pay <=
        this.players[this.p % this.players.length].chip +
          this.players[this.p % this.players.length].bet
      ) {
        if (this.pay >= this.minBet) {
          //アクション
          switch (this.action) {
            case "ベット":
              this.betting();
              break;
            case "コール":
              this.call();
              break;
            case "レイズ":
              this.raise();
              break;
            case "チェック":
              this.check();
              break;
            case "フォールド":
              this.fold();
              break;
            case "オールイン":
              this.allIn();
              break;
          }
        } else if (this.action == "チェック") {
          switch (this.action) {
            case "チェック":
              this.check();
              break;
          }
        } else if (this.action == "フォールド") {
          switch (this.action) {
            case "フォールド":
              this.fold();
              break;
          }
        } else if (this.action == "コール") {
          switch (this.action) {
            case "コール":
              this.call();
              break;
          }
        } else {
          this.comment = "最低ベット額は" + this.minBet + "です";
          this.showErr();
        }
      } else if (this.action == "フォールド") {
        switch (this.action) {
          case "フォールド":
            this.fold();
            break;
        }
      } else if (this.action == "チェック") {
        switch (this.action) {
          case "チェック":
            this.check();
            break;
        }
      } else {
        this.comment = "所持しているチップ数を超えています";
        this.showErr();
      }
    },
    betting() {
      console.log("ベット");
      if (
        Math.max.apply(
          null,
          this.players.map(function(o) {
            return o.bet;
          })
        ) == 0
      ) {
        this.stopTimer();
        this.checkCount = 0;
        this.players[this.p % this.players.length].bet = this.pay;
        this.players[this.p % this.players.length].chip =
          this.players[this.p % this.players.length].chip -
          this.players[this.p % this.players.length].bet;
        console.log(
          "ベット額:" + this.players[this.p % this.players.length].bet
        );
        console.log(
          "チップ:" + this.players[this.p % this.players.length].chip
        );
        this.nextTurn();
      } else {
        this.comment = "既にベットされています";
        this.showErr();
      }
    },
    call() {
      console.log("コール");
      if (
        this.players[this.p % this.players.length].bet <
        Math.max.apply(
          null,
          this.players.map(function(o) {
            return o.bet;
          })
        )
      ) {
        this.stopTimer();
        this.checkCount = 0;
        if (
          Math.max.apply(
            null,
            this.players.map(function(o) {
              return o.isplay;
            })
          ) == 2
        ) {
          this.players[this.p % this.players.length].isplay = 2;
          this.playing--;
        }
        this.pay = Math.max.apply(
          null,
          this.players.map(function(o) {
            return o.bet;
          })
        );
        let pay2 =
          Number(this.pay) - this.players[this.p % this.players.length].bet;
        this.players[this.p % this.players.length].bet = this.pay;
        this.players[this.p % this.players.length].chip =
          this.players[this.p % this.players.length].chip - pay2;
        console.log(
          "ベット額:" + this.players[this.p % this.players.length].bet
        );
        console.log(
          "チップ:" + this.players[this.p % this.players.length].chip
        );
        this.nextTurn();
      } else if (
        Math.max.apply(
          null,
          this.players.map(function(o) {
            return o.bet;
          })
        ) == 0
      ) {
        this.stopTimer();
        this.checkCount = 0;
        if (
          Math.max.apply(
            null,
            this.players.map(function(o) {
              return o.isplay;
            })
          ) == 2
        ) {
          this.players[this.p % this.players.length].isplay = 2;
          this.playing--;
        }
        this.players[this.p % this.players.length].bet = this.pay;
        this.players[this.p % this.players.length].chip =
          this.players[this.p % this.players.length].chip -
          this.players[this.p % this.players.length].bet;
        console.log(
          "ベット額:" + this.players[this.p % this.players.length].bet
        );
        console.log(
          "チップ:" + this.players[this.p % this.players.length].chip
        );
        this.nextTurn();
      } else {
        this.comment = "コールできません";
        this.showErr();
      }
    },
    raise() {
      console.log("レイズ");
      if (
        this.pay >=
        Math.max.apply(
          null,
          this.players.map(function(o) {
            return o.bet;
          })
        )
      ) {
        if (
          Number(this.pay) +
            Number(
              Math.max.apply(
                null,
                this.players.map(function(o) {
                  return o.bet;
                })
              )
            ) <=
          this.players[this.p % this.players.length].chip
        ) {
          this.stopTimer();
          this.checkCount = 0;
          this.pay =
            Number(this.pay) +
            Math.max.apply(
              null,
              this.players.map(function(o) {
                return o.bet;
              })
            );
          let pay2 =
            Number(this.pay) - this.players[this.p % this.players.length].bet;
          this.players[this.p % this.players.length].bet = this.pay;
          this.players[this.p % this.players.length].chip =
            this.players[this.p % this.players.length].chip - pay2;
          console.log(
            "ベット額:" + this.players[this.p % this.players.length].bet
          );
          console.log(
            "チップ:" + this.players[this.p % this.players.length].chip
          );
          this.nextTurn();
        } else {
          this.comment = "チップが足りません";
          this.showErr();
        }
      } else {
        this.comment = "ベットの2倍以上でレイズしてください";
        this.showErr();
      }
    },
    check() {
      console.log("チェック");
      let fp = this.round + 1;
      while (this.players[fp % this.players.length].isplay != 0) {
        fp++;
      }
      if (
        Math.max.apply(
          null,
          this.players.map(function(o) {
            return o.bet;
          })
        ) == 0
      ) {
        this.stopTimer();
        this.checkCount++;
        if (this.checkCount == this.playing) {
          this.checkCount = 0;
          this.showAction();
          this.nextBr();
        } else {
          this.nextTurn();
        }
        //プリフロップbb round+1=bb
      } else if (
        this.br == 0 &&
        this.p % this.players.length == fp % this.players.length
      ) {
        this.showAction();
        this.nextBr();
      } else {
        this.comment = "既にベットされています";
        this.showErr();
      }
    },
    fold() {
      console.log("フォールド");
      this.stopTimer();
      this.players[this.p % this.players.length].isplay = 1;
      console.log(
        this.players[this.p % this.players.length].name + ":フォールド"
      );
      this.playing--;
      this.nextTurn();
    },
    allIn() {
      console.log("オールイン");
      if (
        this.players[this.p % this.players.length].chip +
          this.players[this.p % this.players.length].bet >=
        Math.max.apply(
          null,
          this.players.map(function(o) {
            return o.bet;
          })
        )
      ) {
        this.stopTimer();
        this.checkCount = 0;
        this.players[this.p % this.players.length].bet =
          this.players[this.p % this.players.length].bet +
          this.players[this.p % this.players.length].chip;
        this.players[this.p % this.players.length].chip = 0;
        this.players[this.p % this.players.length].isplay = 2;
        this.playing--;
        console.log(
          "ベット額:" + this.players[this.p % this.players.length].bet
        );
        console.log(
          "チップ:" + this.players[this.p % this.players.length].chip
        );
        this.nextTurn();
      } else {
        this.comment = "チップが足りません";
        this.showErr();
      }
    },
    winner() {
      if (this.win != "" || this.win == 0) {
        this.stopTimer();
        this.players[this.win].chip = this.players[this.win].chip + this.pot;
        this.winComment = this.players[this.win].name + "さんが勝ちました";
        this.$modal.hide("winner-modal");
        this.wc = 0;
        this.nextRound();
      }
    },
    nextTurn() {
      this.showAction();
      this.comment = "";
      //isplayer==0のベットが全て同じか
      let eBet = 0;
      for (let i = 0; i < this.players.length; i++) {
        if (this.players[this.p % this.players.length].isplay == 0) {
          if (
            this.players[this.p % this.players.length].bet ==
            this.players[i].bet
          ) {
            if (this.players[i].bet != 0) {
              eBet++;
            }
          }
        }
      }
      console.log(eBet + "." + this.playing + "." + this.players.length);
      //nextTurn
      if (
        eBet != this.playing ||
        Math.max.apply(
          null,
          this.players.map(function(o) {
            return o.bet;
          })
        ) == 0 ||
        (this.br == 0 &&
          this.p <
            Number(this.players.length + this.round % this.players.length + 1))
      ) {
        console.log("eBet != this.playing ||");
        this.p++;
        //フォールドした人を飛ばす
        while (this.players[this.p % this.players.length].isplay != 0) {
          this.p++;
          if (this.p == this.maxRound + this.players.length) {
            break;
          }
        }
        //全員フォールドしたとき
        if (this.playing == 1) {
          //全員フォールドしたとき
          if (
            Math.max.apply(
              null,
              this.players.map(function(o) {
                return o.isplay;
              })
            ) == 1
          ) {
            for (let i = 0; i < this.players.length; i++) {
              this.allBet = Number(this.allBet) + Number(this.players[i].bet);
              this.players[i].bet = 0;
            }
            this.pot = this.pot + Number(this.allBet);
            this.allBet = 0;
            this.players[this.p % this.players.length].chip =
              this.players[this.p % this.players.length].chip + this.pot;
            this.winComment =
              this.players[this.p % this.players.length].name +
              "さんが勝ちました";
            this.nextRound();
          } else {
            this.stopTimer();
            this.startTimer(); //commentout
            this.turn = this.players[this.p % this.players.length].name;
            console.log(this.turn + "の番");
          }
          //オールイン
        } else if (this.playing == 0) {
          console.log("allincall");
          let ow = 0;
          for (let i = 0; i < this.players.length; i++) {
            this.allBet = Number(this.allBet) + Number(this.players[i].bet);
            this.players[i].bet = 0;
            if (this.players[i].isplay == 2) {
              ow++;
            }
          }
          //オールイン一人
          if (ow == 1) {
            for (let i = 0; i < this.players.length; i++) {
              if (this.players[i].isplay == 2) {
                this.pot = this.pot + Number(this.allBet);
                this.allBet = 0;
                this.players[i].chip = this.players[i].chip + this.pot;
                this.winComment = this.players[i].name + "さんが勝ちました";
                this.nextRound();
              }
            }
          }
          this.pot = this.pot + Number(this.allBet);
          this.allBet = 0;
          this.show();
        } else {
          this.stopTimer();
          this.startTimer(); //comment
          this.turn = this.players[this.p % this.players.length].name;
          console.log(this.turn + "の番");
        }
      } else {
        console.log("else");
        if (this.playing == 0) {
          let ow = 0;
          for (let i = 0; i < this.players.length; i++) {
            this.allBet = Number(this.allBet) + Number(this.players[i].bet);
            this.players[i].bet = 0;
            if (this.players[i].isplay == 2) {
              ow++;
            }
          }
          //オールイン一人
          if (ow == 1) {
            this.pot = this.pot + Number(this.allBet);
            this.allBet = 0;
            for (let i = 0; i < this.players.length; i++) {
              if (this.players[i].isplay == 2) {
                console.log("オールイン" + this.players[i].name);
                this.players[i].chip = this.players[i].chip + this.pot;
                this.winComment = this.players[i].name + "さんが勝ちました";
                this.nextRound();
              }
            }
          } else {
            this.pot = this.pot + Number(this.allBet);
            this.allBet = 0;
            this.show();
          }
        } else {
          this.nextBr();
        }
      }
    },
    nextBr() {
      //ベットをポットに移動
      for (let i = 0; i < this.players.length; i++) {
        this.allBet = Number(this.allBet) + Number(this.players[i].bet);
        this.players[i].bet = 0;
      }
      this.pot = this.pot + Number(this.allBet);
      this.allBet = 0;
      if (this.br < 3) {
        //ベッティングラウンドを進める
        this.br = this.br + 1;
        console.log(this.bettingRound[this.br]);
        this.p = this.round % this.players.length;
        while (this.players[this.p % this.players.length].isplay != 0) {
          this.p++;
          if (this.p == this.maxRound + this.players.length) {
            break;
          }
        }
        this.stopTimer();
        this.startTimer(); //commentout
        this.turn = this.players[this.p % this.players.length].name;
        console.log(this.turn + "の番");
      } else {
        if (this.action != "フォールド") {
          this.show();
        }
      }
    },
    nextRound() {
      //次のラウンド・ディーラーを回す
      if (this.round < this.maxRound) {
        this.round += 1;
        this.pot = 0;
        this.br = 0;
        this.playing = this.players.length;
        for (let i = 0; i < this.players.length; i++) {
          if (this.players[i].chip > 0) {
            this.players[i].isplay = 0;
          } else {
            this.players[i].isplay = 1;
            this.playing--;
          }
          if (this.playing == 1) {
            this.sort();
            this.stopTimer();
            this.$store.commit("navigator/push", page3);
          }
        }
        this.p = (this.round - 1) % this.players.length;
        while (this.players[this.p % this.players.length].isplay == 1) {
          this.p++;
        }
        this.dealer = this.players[this.p % this.players.length].name;
        //コンソール出力
        console.log("ディーラー:" + this.dealer);
        console.log(this.bettingRound[0]);
        //SB.BBのベット
        this.sbbb();
      } else {
        this.sort();
        //結果のページに遷移
        this.stopTimer();
        this.$store.commit("navigator/push", page3);
      }
    },
    sbbb() {
      //sb
      this.p = this.round % this.players.length;
      while (this.players[this.p % this.players.length].isplay != 0) {
        this.p++;
      }
      this.players[this.p % this.players.length].bet = this.minBet / 2;
      this.players[this.p % this.players.length].chip =
        this.players[this.p % this.players.length].chip -
        this.players[this.p % this.players.length].bet;
      console.log(this.players[this.p % this.players.length].name + "の番");
      console.log("ベット額:" + this.players[this.p % this.players.length].bet);
      console.log("チップ:" + this.players[this.p % this.players.length].chip);
      //bb
      this.p++;
      while (this.players[this.p % this.players.length].isplay != 0) {
        this.p++;
      }
      this.players[this.p % this.players.length].bet = this.minBet;
      this.players[this.p % this.players.length].chip =
        this.players[this.p % this.players.length].chip -
        this.players[this.p % this.players.length].bet;
      console.log(this.players[this.p % this.players.length].name + "の番");
      console.log("ベット額:" + this.players[this.p % this.players.length].bet);
      console.log("チップ:" + this.players[this.p % this.players.length].chip);
      //utg
      this.p++;
      while (this.players[this.p % this.players.length].isplay != 0) {
        this.p++;
      }
      this.turn = this.players[this.p % this.players.length].name;
      console.log(this.players[this.p % this.players.length].name + "の番");
      this.stopTimer();
      this.startTimer(); //commentout
    },
    show() {
      this.wc++;
      this.startTimerWinner();
      this.$modal.show("winner-modal");
    },
    sort() {
      console.log(this.players);
      this.players.sort(function(a, b) {
        if (a.chip > b.chip) return -1;
        if (a.chip < b.chip) return 1;
        return 0;
      });
      this.$store.state.ranking = this.players;
    },
    fetch() {
      let that = this;
      console.log("fetch" + this.w);
      fetch(
        this.$url + "/record" + "?recordID=" + localStorage.getItem("recordID"),
        { method: "GET" }
      )
        .then(res => {
          // 返されたBodyをjsonにしてPromise.resolve()する
          return res.json();
        })
        .then(data => {
          // api_url から返されたデータ(json)
          // 実際にデータを加工したり色々する
          console.log(data);
          that.action = data.record.action.value;
          if (that.action == "レイズ" || that.action == "ベット") {
            that.pay = data.record.point.value;
          }
          that.update = data.record.time.value;
        })
        .catch(err => {
          console.error(err);
        });
    },
    startTimer() {
      let that = this;
      console.log("interval");
      that.timer = setInterval(function() {
        that.fetch();
      }, 3000);
    },
    stopTimer() {
      let that = this;
      clearInterval(this.timer);
      console.log("stopped");
    },
    fetchWinner() {
      let that = this;
      console.log("fetchWinner");
      fetch(
        this.$url + "/record" + "?recordID=" + localStorage.getItem("recordID"),
        { method: "GET" }
      )
        .then(res => {
          // 返されたBodyをjsonにしてPromise.resolve()する
          return res.json();
        })
        .then(data => {
          // api_url から返されたデータ(json)
          // 実際にデータを加工したり色々する
          console.log(data);
          if (data.record.winner.value != "") {
            this.win = data.record.winner.value - 1;
            console.log(this.win);
          }
        })
        .catch(err => {
          console.error(err);
        });
    },
    startTimerWinner() {
      let that = this;
      console.log(this.wc);
      that.timer = setInterval(function() {
        that.fetchWinner();
      }, 3000);
    },
    winner2() {
      this.win = this.selectWinnerValue;
    },
    async showAction() {
      let that = this;
      this.$modal.show("action-modal");
      await setTimeout(function() {
        that.$modal.hide("action-modal");
      }, 2000);
    },
    showErr() {
      let that = this;
      this.$modal.show("err-modal");
      setTimeout(function() {
        that.$modal.hide("err-modal");
      }, 2000);
    }
  }
};
</script>


<style scoped>
/* 奥瀬が教えてくれたんご */
@import url(https://cdnjs.cloudflare.com/ajax/libs/animate.css/3.7.2/animate.min.css);
.gradation {
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
.pod {
  vertical-align: middle;
}
.bet {
  vertical-align: middle;
}
.flex_box1 {
  display: flex;
  justify-content: space-around;
}

.text_content {
  width:auto;
  padding: 0%;

}
.table_content {
  /* margin-right: 10px; */
  padding-right: 20%;
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
.active {
  background-color: red;
}
.isfold {
  background-color: blueviolet;
}

.preflop {
  background-color: rgb(223, 134, 226);
}
.flop {
  background-color: rgb(223, 134, 226);
}
.turnCL {
  background-color: rgb(223, 134, 226);
}
.river {
  background-color: rgb(223, 134, 226);
}

/* テーブル画像について */
.flex_box2 {
  display: flex;
  flex-direction: column;
  padding-top: 36px;
}
.imgtable-content {
  position: relative;
}
.table-text-center{
  position: absolute;
  top: 32%;
  left: 38%;
  padding: 10px;
  background-color: #d4f0fd
}
.table-text-player{
  background-color: #d4f0fd
}
.table-player0{
  position: absolute;
  top: 76%;
  left: 27%;
  background-color: #d4f0fd
}
.table-player1{
  position: absolute;
  top: 76%;
  left: 58%;
  background-color: #d4f0fd
}
.table-player2{
  position: absolute;
  top: 3%;
  left: 27%;
  background-color: #d4f0fd
}
.table-player3{
  position: absolute;
  top: 3%;
  left: 58%;
  background-color: #d4f0fd
}
.table-player4{
  position: absolute;
  top: 60%;
  left: 7%;
  background-color: #d4f0fd
}
.table-player5{
  position: absolute;
  top: 22%;
  left: 82%;
  background-color: #d4f0fd
}
.table-player6{
  position: absolute;
  top: 60%;
  left: 82%;
  background-color: #d4f0fd
}
.table-player7{
  position: absolute;
  top: 22%;
  left: 7%;
  background-color: #d4f0fd
}
.table-player8{
  position: absolute;
  top: 3%;
  left:43%;
  background-color: #d4f0fd
}
.table-player9{
  position: absolute;
  top: 76%;
  left:43%;
  background-color: #d4f0fd
}





</style>
