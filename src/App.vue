<template>
  <div id="app" @click="refocusInput">
    <header>
      <h1>Bellroy Robot Simulator</h1>
      <p>Author: Faisal Santosa, 11 Aug 2024</p>
    </header>
    <div class="grid-container">
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
body {
  font-family: "Roboto", sans-serif;
  background-color: #f2f2f2;
}

header {
  /* display: flex;
  align-items: center;
  justify-content: center; */
  padding: 20px;
  background-color: #ffffff;
  border-bottom: 2px solid #e0e0e0;
  text-align: center;
}

.logo {
  width: 100px;
  margin-right: 10px;
}

h1 {
  font-size: 24px;
  color: #333333;
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
  display: flex;
  /* justify-content: center; */
  flex-direction: column;
  align-items: center;
  gap: 20px;
  margin-top: 20px;
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

</style>
