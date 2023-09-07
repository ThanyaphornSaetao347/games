<template>
  <div>
    <h1 style="color: #14252C;">เกมเป่ายิ้งฉุบ</h1>
    <div class="choices">
      <div class="choice">
        <div>
          <img v-if="playerChoice === 'ค้อน'" src="./assets/ค้อน.png" alt="ค้อน" />
          <img v-if="playerChoice === 'กระดาษ'" src="./assets/กระดาษ.png" alt="กระดาษ" />
          <img v-if="playerChoice === 'กรรไกร'" src="./assets/กรรไกร.png" alt="กรรไกร" />
        </div>
        <br>
        <br>
        <br>
        <p class="choice-label">
          คุณ:{{ playerChoice }}</p>
      </div>
      <div class="choice">
        <div>
          <img v-if="computerChoice === 'ค้อน'" src="./assets/ค้อน.png" alt="ค้อน" />
          <img v-if="computerChoice === 'กระดาษ'" src="./assets/กระดาษ.png" alt="กระดาษ" />
          <img v-if="computerChoice === 'กรรไกร'" src="./assets/กรรไกร.png" alt="กรรไกร" />
        </div>
        <br>
        <br>
        <br>
        <p class="choice-label">
          คอมพิวเตอร์:{{ computerChoice }}</p>
      </div>
    </div>
    <div>
      <p style="font-size: 18px;">ผู้ชนะคือ!!: {{ result }}</p>
      <div class="score">
        <p>{{ `คะแนน ${playerScore}:${computerScore}` }}</p>
      </div>
      <div class="buttons">
        <button @click="playGame" class="color-box1">เป่ายิ้งงงงงงงงง ฉุบ!</button>
        <button @click="resetGame" class="color-box2">เริ่มใหม่จ้าาา</button>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue'

  export default {
  data() {
    return {
      playerChoice: null,
      computerChoice: null,
      result: null,
      playerScore: 0,  // เพิ่มตัวแปรคะแนนผู้เล่น
      computerScore: 0,  // เพิ่มตัวแปรคะแนนคอมพิวเตอร์
    };
  },
  methods: {
    playGame() {
      // random
      function computerChoice() {
        const choices = ["ค้อน", "กรรไกร", "กระดาษ"];
        return choices[Math.floor(Math.random() * choices.length)];
      }

      // สร้างค่าสำหรับผู้เล่นและคอมพิวเตอร์
      this.playerChoice = this.getRandomChoice();
      this.computerChoice = computerChoice();

      //เปรียบเทียบผลลัพธ์
      function compare(playerChoice, computerChoice) {
        if (playerChoice === computerChoice) {
          return "เสมอเนาะ";
        } else if (
          (playerChoice === "ค้อน" && computerChoice === "กรรไกร") ||
          (playerChoice === "กรรไกร" && computerChoice === "กระดาษ") ||
          (playerChoice === "กระดาษ" && computerChoice === "ค้อน")
        ) {
          return "คุณไง";
        } else {
          return "คอมพิวเตอร์จ้า";
        }
      }

      // คำนวณผลลัพธ์
      this.result = compare(this.playerChoice, this.computerChoice);
  
      // อัพเดทคะแนน
      if (this.result === "คุณไง") {
        this.playerScore += 1;
      } else if (this.result === "คอมพิวเตอร์จ้า") {
        this.computerScore += 1;
      }
    },
    resetGame() {
      // รีเซ็ตเกมใหม่
      this.playerChoice = null;
      this.computerChoice = null;
      this.result = null;
      // เริ่มนับคะแนนใหม่
      this.playerScore = 0;
      this.computerScore = 0;
    },
    getRandomChoice() {
      const choices = ["ค้อน", "กรรไกร", "กระดาษ"];
      return choices[Math.floor(Math.random() * choices.length)];
    },
  },
};
</script>

<style scoped>
h1 {
  text-align: center;
}
.buttons {
  display: flex;
  justify-content: center; /* จัดปุ่มไปทางซ้าย */
  gap: 10px; /* ระยะห่างระหว่างปุ่ม */
  font-size: 18px;
}

.choices {
  display: flex;
  justify-content: space-around;
}

.choice {
  text-align: center;
  margin: 10px;
  position: relative;
}

.choice img {
  max-width: 200px;
  max-height: 200px;
  margin: 0 auto;
  display: block;
}

.choice p.choice-label {
  position: absolute;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
  margin-top: 10px;
  font-size: 18px;
}
.player-choice,.computer-choice {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.score {
  text-align: center;
  font-size: 19px;
  margin-bottom: 20px;
  background-color: #A58E74;
  color: white;
  margin: 35px;
  border-radius: 10px; 
}
.score-label {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
}

.score-label::before,.score-label::after {
  content: "";
  flex: 1;
  height: 2px;
  background-color: #000;
  margin: 0 10px;
}

.score-label span {
  font-weight: bold;
  font-size: 20px;
}
.color-box1{
  background-color:#424530;
  color: white;
}
.color-box2{
  background-color:#FFEFCD ;
}

</style>