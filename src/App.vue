<template>
  <div id="app" @click="refocusInput">
    <header>
      <h1>Bellroy Robot Simulator</h1>
      <small>Author: Faisal Santosa, </small>
      <small>Email: fmulya89@gmail.com</small>
    </header>
    <div class="grid-container box">
      <div v-for="(row, rowIndex) in 5" :key="rowIndex" class="grid-row">
        <div
          v-for="(col, colIndex) in 5"
          :key="colIndex"
          class="grid-cell"
          :class="{ robot: isRobotPosition(rowIndex, colIndex) }"
        >
          <span v-if="isRobotPosition(rowIndex, colIndex)">
            {{ arrowCharacter }}
          </span>
        </div>
      </div>
    </div>
    <div class="controls">
      <!-- <button @click="moveForward">Move Forward</button>
      <button @click="rotateLeft">Rotate Left</button>
      <button @click="rotateRight">Rotate Right</button> -->
      <p>Move using keyboard WSAD</p>
      <p>
        <img src="../src/assets/wasd.png" />
      </p>
    </div>
    <div>
    </div>
    <!-- Hidden input to capture key events -->
    <input
      type="text"
      class="hidden-input"
      @keydown="handleKeydown"
      ref="hiddenInput"
      autofocus
    />
  </div>
</template>

<script>
// import HelloWorldVue from "./components/HelloWorld.vue";
export default {
  name: "App",
  components: {
    // HelloWorld: HelloWorldVue,
  },
  data() {
    return {
      robot: {
        x: 0,
        y: 0,
        direction: "N", // N, E, S, W
      },
    };
  },
  computed: {
    arrowCharacter() {
      switch (this.robot.direction) {
        case "N":
          return "↑";
        case "E":
          return "→";
        case "S":
          return "↓";
        case "W":
          return "←";
        default:
          return "";
      }
    },
  },
  methods: {
    isRobotPosition(row, col) {
      return this.robot.y === row && this.robot.x === col;
    },
    moveForward() {
      if (this.robot.direction === "N" && this.robot.y > 0) this.robot.y--;
      if (this.robot.direction === "S" && this.robot.y < 4) this.robot.y++;
      if (this.robot.direction === "E" && this.robot.x < 4) this.robot.x++;
      if (this.robot.direction === "W" && this.robot.x > 0) this.robot.x--;
    },
    rotateLeft() {
      const directions = ["N", "W", "S", "E"];
      const currentIndex = directions.indexOf(this.robot.direction);
      this.robot.direction = directions[(currentIndex + 1) % 4];
    },
    rotateRight() {
      const directions = ["N", "E", "S", "W"];
      const currentIndex = directions.indexOf(this.robot.direction);
      this.robot.direction = directions[(currentIndex + 1) % 4];
    },
    handleKeydown(event) {
      switch (event.key) {
        case "w":
          // Move Forward
          if (this.robot.direction === "N" && this.robot.y > 0) this.robot.y--;
          if (this.robot.direction === "S" && this.robot.y < 4) this.robot.y++;
          if (this.robot.direction === "E" && this.robot.x < 4) this.robot.x++;
          if (this.robot.direction === "W" && this.robot.x > 0) this.robot.x--;
          break;
        case "a":
          // Rotate Left
          this.rotateLeft();
          break;
        case "d":
          // Rotate Right
          this.rotateRight();
          break;
        case "s":
          // Move Backward
          if (this.robot.direction === "N" && this.robot.y < 4) this.robot.y++;
          if (this.robot.direction === "S" && this.robot.y > 0) this.robot.y--;
          if (this.robot.direction === "E" && this.robot.x > 0) this.robot.x--;
          if (this.robot.direction === "W" && this.robot.x < 4) this.robot.x++;
          break;
      }
    },
    refocusInput() {
      // Refocus the hidden input element whenever the page is clicked
      this.$refs.hiddenInput.focus();
    },
  },
};
</script>

<style>
html{
  background: #0A0A0A;
}
body {
  font-family: "Roboto", sans-serif;
  /* background-color: #f2f2f2; */
}

header {
  padding: .5rem;
  background-color: #12181F;
  color: #EDEDED;
  text-align: center;
}

.logo {
  width: 100px;
  margin-right: 10px;
}

h1 {
  font-size: 24px;
}

.grid-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: 20px 0;
}

.grid-row {
  display: flex;
}

.grid-cell {
  width: 60px;
  height: 60px;
  border: 1px solid #ccc;
  display: flex;
  align-items: center;
  justify-content: center;
}

.robot {
  background-color: #007acc;
  color: #ffffff;
  font-size: 24px;
}

.controls {
  color: #EDEDED;
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 20px;
}
.controls p{
  margin: 0;
}
.controls img{
  filter: invert(1);
}

button {
  padding: 10px 20px;
  background-color: #007acc;
  color: #ffffff;
  border: none;
  cursor: pointer;
  font-size: 16px;
}

button:hover {
  background-color: #005ea6;
}

.hidden-input {
  position: absolute;
  left: -9999px;
}
.box {
  padding: 2rem;
  --border-size: 3px;
  --border-angle: 0turn;
  background-image: conic-gradient(from var(--border-angle), #213, #112 50%, #213), conic-gradient(from var(--border-angle), transparent 20%, #08f, #f03);
  background-size: calc(100% - (var(--border-size) * 2)) calc(100% - (var(--border-size) * 2)), cover;
  background-position: center center;
  background-repeat: no-repeat;
  -webkit-animation: bg-spin 3s linear infinite;
          animation: bg-spin 3s linear infinite;
}
@-webkit-keyframes bg-spin {
  to {
    --border-angle: 1turn;
  }
}
@keyframes bg-spin {
  to {
    --border-angle: 1turn;
  }
}
.box:hover {
  -webkit-animation-play-state: paused;
          animation-play-state: paused;
}

@property --border-angle {
  syntax: "<angle>";
  inherits: true;
  initial-value: 0turn;
}
</style>
