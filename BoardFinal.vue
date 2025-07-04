<script setup>
import { watch } from 'vue'
import { ref } from 'vue'

const cells = ref(['', '', '', '', '', '', '', '', ''])

// const msg = ref('Hello Killua!');
const turn = ref('X')
// const winner = ref()
const disableWinner = ref(false)

// const wow = ref(false);
const indx = ref()
const toBeRemoved = ref([])

const play = (x) => {
  if (cells.value[x] == '') {
    cells.value[x] = turn.value
    if (turn.value === 'X') turn.value = 'O'
    else if (turn.value === 'O') turn.value = 'X'
    //toBeRemoved queue
    toBeRemoved.value.push(x)
    if (toBeRemoved.value.length > 6) {
      indx.value = toBeRemoved.value[0]
      cells.value[indx.value] = ''
      toBeRemoved.value.shift()
    }
  }
}

const resetBoard = () => {
  cells.value = ['', '', '', '', '', '', '', '', '']
  toBeRemoved.value = []
  turn.value = 'X'
  disableWinner.value = false
}

const finalWin = ref()

//  computed(() => calculateWin(cells.value))

const updateWin = (cells) => {
  const winningPos = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
  ]
  for (let i = 0; i < winningPos.length; i++) {
    const [a, b, c] = winningPos[i]
    if (cells[a] && cells[a] == cells[b] && cells[c] == cells[b]) {
      disableWinner.value = true
      finalWin.value = cells[a]
    }
  }
}
watch(cells, updateWin, { deep: true })
</script>

<template>
  <link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Audiowide|Sofia|Trirong" />
  <div class="center">
    <div v-if="!finalWin">
      <h3>{{ turn }}'s Turn</h3>
    </div>

    <!-- <div v-if="wow">
    <h3>Trying</h3>
      </div> -->

    <div v-if="finalWin">
      <h3>{{ finalWin }} is the Winner!!</h3>
    </div>
    <div class="row">
      <button class="container" @click.stop="play(0)" :disabled="disableWinner">
        {{ cells[0] }}
      </button>
      <button class="container" @click.stop="play(1)" :disabled="disableWinner">
        {{ cells[1] }}
      </button>
      <button class="container" @click.stop="play(2)" :disabled="disableWinner">
        {{ cells[2] }}
      </button>
    </div>
    <div class="row">
      <button class="container" @click.stop="play(3)" :disabled="disableWinner">
        {{ cells[3] }}
      </button>
      <button class="container" @click.stop="play(4)" :disabled="disableWinner">
        {{ cells[4] }}
      </button>
      <button class="container" @click.stop="play(5)" :disabled="disableWinner">
        {{ cells[5] }}
      </button>
    </div>
    <div class="row">
      <button class="container" @click.stop="play(6)" :disabled="disableWinner">
        {{ cells[6] }}
      </button>
      <button class="container" @click.stop="play(7)" :disabled="disableWinner">
        {{ cells[7] }}
      </button>
      <button class="container" @click.stop="play(8)" :disabled="disableWinner">
        {{ cells[8] }}
      </button>
    </div>

    <div class="resetBtn">
      <button class="audioWide" @click.stop="resetBoard()">Reset</button>
    </div>
  </div>
</template>

<style>
.row {
  display: flex;
  position: relative;
  margin: auto;
  width: 50%;
  justify-content: center;
}
.container {
  width: 60px;
  height: 60px;
  border: 1px solid;
  font-family: 'Audiowide', sans-serif;
  font-size: 30px;
  text-shadow: 3px 3px 3px #ababab;
  text-align: center;
  vertical-align: middle;
  display: flex;
  justify-content: center;
  align-items: center;
}
h3 {
  font-family: monospace;
}
.center {
  margin: auto;
  width: 50%;
  text-align: center;
}
.resetBtn {
  margin-top: 10px;
}
.audioWide {
  font-family: monospace;
}
</style>
