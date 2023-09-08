<template>
  <div id="app">
    <h1 style="font-size: 70px;">เป่ายิ้งฉุบ</h1>
    <h2>Player 1 vs Player 2</h2>
    <div>
      <p>Player 1 score: {{ player1Score }}</p>
      <p>Player 2 score: {{ player2Score }}</p>
    </div>
    <div>
      <button class="buttons" @click="playGame">เป่ายิ้งฉุบ!</button>
      <button class="buttons" @click="resetGame">รีเซ็ต</button>
    </div>
    <div>
      <p v-if="result !== null">ผลลัพธ์: {{ result }}</p>
    </div>
    <div>
      <img v-if="player1Choice" :src="player1ChoiceImage" alt="Player 1's Choice" />
      <img v-if="player2Choice" :src="player2ChoiceImage" alt="Player 2's Choice" />
    </div>

  </div>
</template>

<script>
export default {
  data() {
    return {
      player1Score: 0,
      player2Score: 0,
      result: null,
      player1Choice: null,
      player2Choice: null,
    };
  },
  computed: {
    player1ChoiceImage() {
      return this.player1Choice ? `/images/${this.player1Choice.toLowerCase()}.png` : '';
    },
    player2ChoiceImage() {
      return this.player2Choice ? `/images/${this.player2Choice.toLowerCase()}.png` : '';
    },
  },
  methods: {
    playGame() {
      const options = ["ค้อน", "กรรไกร", "กระดาษ", "ความรัก"];
      this.player1Choice = options[Math.floor(Math.random() * 4)];
      this.player2Choice = options[Math.floor(Math.random() * 4)];

      if (this.player1Choice === this.player2Choice) {
        this.result = "เสมอ";
      } else if (this.player1Choice === "ความรัก"){
        this.result = "ความรักชนะเสมอ!";
        this.player1Score += 1;
      
      } else if (this.player2Choice === "ความรัก"){
        this.result = "ความรักชนะเสมอ!";
        this.player2Score += 1;
      } else if (
        (this.player1Choice === "ค้อน" && this.player2Choice === "กรรไกร") ||
        (this.player1Choice === "กรรไกร" && this.player2Choice === "กระดาษ") ||
        (this.player1Choice === "กระดาษ" && this.player2Choice === "ค้อน")
      ) {
        this.result = "Player 1 ชนะ!";
        this.player1Score += 1;
      } else {
        this.result = "Player 2 ชนะ!";
        this.player2Score += 1;
      }
    },
    resetGame() {
      this.player1Score = 0;
      this.player2Score = 0;
      this.result = null;
      this.player1Choice = null;
      this.player2Choice = null;
    },
  },
};
</script>

<style>
#app {
  text-align: center;
  margin-top: 20px;
}

button {
  margin: 10px;
  padding: 10px 20px;
  font-size: 16px;
}

.buttons {
  margin: 10px;
  padding: 10px 20px;
  font-size: 16px;
}

div p {
  font-size: 18px;
}

h1 {
  font-size: 24px;
}
</style>