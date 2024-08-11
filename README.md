# Robot Simulator

This project is a robot simulator built using Vue.js. The robot can be controlled on a 5x5 grid, where it can move forward in the direction it's facing or rotate to face different cardinal directions. The simulator is designed with a Bellroy-inspired aesthetic.

## Demo
Demo [Click Here](https://moonlit-pegasus-c90283.netlify.app/).


## Table of Contents

- [Installation](#installation)
- [Usage](#usage)

## Installation

To get started with the Bellroy Robot Simulator, you need to have [Node.js](https://nodejs.org/) installed. Follow the steps below:

### Clone the repository:


```sh
git clone https://github.com/Ichalle/robot-grid-simulations.git
cd robot-grid-simulations
```


```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Compile and Minify for Production

```sh
npm run build
```

### Lint with [ESLint](https://eslint.org/)

```sh
npm run lint
```

## Usage
Once the simulator is running, you'll see a 5x5 grid with a robot initially positioned at the top-left corner facing north. You can control the robot using the buttons on the screen or with your keyboard.

### Controls
W Key / Move Forward Button: Moves the robot one step forward in the direction it is currently facing.
A Key / Rotate Left Button: Rotates the robot 90 degrees counterclockwise.
D Key / Rotate Right Button: Rotates the robot 90 degrees clockwise.
