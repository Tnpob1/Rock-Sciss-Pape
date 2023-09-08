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
      return this.player1Choice
        ? `/images/${this.player1Choice.toLowerCase()}.png`
        : "";
    },
    player2ChoiceImage() {
      return this.player2Choice
        ? `/images/${this.player2Choice.toLowerCase()}.png`
        : "";
    },
  },
  methods: {
    playGame() {
      const options = ["ค้อน", "กรรไกร", "กระดาษ", "ความรัก"];
      this.player1Choice = options[Math.floor(Math.random() * 4)];
      this.player2Choice = options[Math.floor(Math.random() * 4)];

      if (this.player1Choice === this.player2Choice) {
        this.result = "เสมอ";
      } else if (this.player1Choice === "ความรัก") {
        this.result = "ความรักชนะเสมอ!";
        this.player1Score += 1;
      } else if (this.player2Choice === "ความรัก") {
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

<template>
  <div class="w-full flex flex-col items-center gap-8 my-8">
    <div class="px-24 py-10 rounded-3xl bg-[#FFC0CB]">
      <h1 class="text-6xl font-bold text-white">เป่ายิ้งฉุบ</h1>
    </div>
    <div>
      <h2 class="text-2xl font-semibold">
        <span class="text-blue-600">Player 1</span> vs
        <span class="text-red-600">Player 2</span>
      </h2>
    </div>
    <div class="flex flex-col gap-2">
      <p class="text-blue-600">Player 1 score: {{ player1Score }}</p>
      <p class="text-red-600">Player 2 score: {{ player2Score }}</p>
    </div>
    <div class="flex gap-10">
      <button class="btn" @click="playGame">เป่ายิ้งฉุบ!</button>
      <button class="btn" @click="resetGame">รีเซ็ต</button>
    </div>
    <div class="bg-pink-400 px-6 py-4 text-white rounded-lg shadow-xl">
      <p>
        ผลลัพธ์: <span v-if="result !== null">{{ result }}</span>
      </p>
    </div>
    <div class="grid md:grid-cols-2 gap-6">
      <div class="flex flex-col justify-center gap-2">
        <p class="text-center font-semibold text-blue-600">player 1</p>
        <div class="w-64 h-64 flex items-center justify-center">
          <img
            v-if="player1Choice"
            :src="player1ChoiceImage"
            alt="Player 1's Choice"
            class="object-cover"
          />
        </div>
      </div>
      <div class="flex flex-col justify-center gap-2">
        <p class="text-center font-semibold text-red-600">player 2</p>
        <div class="w-64 h-64 flex items-center justify-center">
          <img
            v-if="player2Choice"
            :src="player2ChoiceImage"
            alt="Player 2's Choice"
            class="object-cover"
          />
        </div>
      </div>
    </div>
  </div>
</template>
