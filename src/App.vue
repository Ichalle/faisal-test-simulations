<template>
  <header>
    <h1>Bellroy Robot Simulator</h1>
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
};
</script>
<style>
body {
  font-family: "Roboto", sans-serif;
  background-color: #f2f2f2;
}

header {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20px;
  background-color: #ffffff;
  border-bottom: 2px solid #e0e0e0;
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
</style>
