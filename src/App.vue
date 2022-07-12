<script setup lang="ts">
import { reactive, ref } from "vue";

import GamersList from "@/components/GamersList.vue";

const gamers = ref<Array<string>>([
  "Dawid",
  "Marcin W",
  "Marcin B",
  "Grzegorz",
  "Patryk",
  "Mateusz",
]);

const checkedPlayers = ref<Array<string | null>>([]);
const playersOnBoard = ref<Array<object | null>>([]);

const showBoard = ref<boolean>(false);

const genRandNumber = () => Math.random() * checkedPlayers.value.length;

function handleCheck(val: string) {
  showBoard.value = false;

  if (checkedPlayers.value.find((elem) => elem === val)) {
    checkedPlayers.value = checkedPlayers.value.filter(
      (player) => player !== val
    );
  } else {
    checkedPlayers.value.push(val);
  }
}

function generateTeams() {
  for (let i: number = 0; i < checkedPlayers.value.length; i++) {
    playersOnBoard.value[i] = {
      name: checkedPlayers.value[i],
      id: genRandNumber(),
    };
  }
  playersOnBoard.value.sort((a, b) => a.id - b.id);
  showBoard.value = true;
}
</script>

<template>
  <main class="app">
    <h1 class="title">Team Creator</h1>

    <div class="row">
      <div class="sidebar">
        <GamersList
          :availableGamers="gamers"
          :checkedPlayers="checkedPlayers"
          @handleCheck="handleCheck"
        />
        <div class="btn" @click="generateTeams">Generate</div>
      </div>

      <div class="board" v-if="showBoard">
        <div class="player">
          <span>{{ playersOnBoard[0].name }}</span>
          <span>Defence</span>
        </div>
        <div class="player">
          <span>{{ playersOnBoard[1].name }}</span>
          <span>Attack</span>
        </div>
        <div class="divider"></div>
        <div class="player">
          <span>Attack</span>
          <span>{{ playersOnBoard[2].name }}</span>
        </div>
        <div class="player">
          <span>Defence</span>
          <span>{{ playersOnBoard[3].name }}</span>
        </div>
      </div>
    </div>
  </main>
</template>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  color: White;
  font-weight: 500;
}

.app {
  min-height: 100vh;
  width: 100vw;
  margin: 0;
  background-color: #00a752;
  display: flex;
  align-items: center;
  flex-direction: column;
}

.title {
  padding-top: 30px;
  font-size: 32px;
  font-weight: 700;
}

.row {
  display: flex;
  align-items: center;
  justify-content: center;
  min-width: 100%;
  column-gap: 15%;
  padding: 100px 200px;
}

.sidebar {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.btn {
  font-size: 24px;
  height: 40px;
  padding-top: 100px;
  font-weight: 700;
  cursor: pointer;
}
.btn:hover {
  color: #890404;
}

.board {
  height: 500px;
  width: 300px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-evenly;
  border: 2px solid white;
}
.divider {
  position: relative;
  height: 2px;
  width: 100%;
  background-color: #fff;
}
.divider::before {
  position: absolute;
  content: "";
  left: 50%;
  bottom: -7px;
  height: 12px;
  width: 12px;
  border-radius: 50%;
  border: 2px solid white;
  background-color: #00a752;
  transform: translateX(-50%);
}
.player {
  display: flex;
  flex-direction: column-reverse;
  row-gap: 10px;
  align-items: center;
}
.board div:nth-of-type(1) > span,
.board div:nth-of-type(5) > span {
  color: blue;
}
.board div:nth-of-type(2) > span,
.board div:nth-of-type(4) > span {
  color: darkred;
}
@media (max-width: 850px) {
  .row {
    flex-direction: column;
    padding: 50px;
    justify-content: center;
  }
  .btn {
    padding: 20px;
  }
  .board {
    margin-top: 20px;
  }
}
</style>
