<template>
  <div class="word-search" :style="{ width: `${width}px`, height: `${height}px` }">
    <div
      v-for="(row, rowIndex) in grid"
      :key="'row-' + rowIndex"
      class="row"
    >
      <div
        v-for="(cell, colIndex) in row"
        :key="'cell-' + rowIndex + '-' + colIndex"
        class="cell"
        :style="{
          width: `${cellWidth}px`,
          height: `${cellHeight}px`,
          fontSize: `${Math.min(cellWidth, cellHeight) * 0.6}px`,
        }"
      >
        {{ cell }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      across: 15, // Number of columns
      down: 15, // Number of rows
      reversible: false, // Allow words to be placed backwards
      width: 600, // Width of the grid area in pixels
      height: 600, // Height of the grid area in pixels
      show: true, // Highlight words from the list in green
      words: [
        "HOT",
        "CHOCOLATE",
        "GINGER",
        "LATTE",
        "PINE",
        "RED",
        "GREEN",
        "BERRIES",
        "WARM",
        "COOKIE",
        "SCARF",
        "MITTENS",
        "FIREPLACE",
        "GLOVES",
      ],
      grid: [],
      directions: [
        { dx: 1, dy: 0 }, // Right
        { dx: 0, dy: 1 }, // Down
      ],
      letters: "ABCDEFGHIJKLMNOPQRSTUVWXYZ",
    };
  },
  computed: {
    cellWidth() {
      return this.width / this.across;
    },
    cellHeight() {
      return this.height / this.down;
    },
  },
  mounted() {
    this.generateGrid();
  },
  methods: {
    initializeGrid() {
      this.grid = Array.from({ length: this.down }, () =>
        Array.from({ length: this.across }, () => " ")
      );
    },
    fits(word, x, y, dx, dy) {
      for (let i = 0; i < word.length; i++) {
        const nx = x + i * dx;
        const ny = y + i * dy;
        if (
          nx < 0 ||
          ny < 0 ||
          nx >= this.across ||
          ny >= this.down ||
          (this.grid[ny][nx] !== " " && this.grid[ny][nx] !== word[i])
        ) {
          return false;
        }
      }
      return true;
    },
    placeWord(word, x, y, dx, dy) {
      for (let i = 0; i < word.length; i++) {
        const nx = x + i * dx;
        const ny = y + i * dy;
        this.grid[ny][nx] = word[i];
      }
    },
    fillGrid() {
      for (let y = 0; y < this.down; y++) {
        for (let x = 0; x < this.across; x++) {
          if (this.grid[y][x] === " ") {
            const randomLetter =
              this.letters[Math.floor(Math.random() * this.letters.length)];
            this.grid[y][x] = randomLetter;
          }
        }
      }
    },
    generateGrid() {
      this.initializeGrid();
      this.words = this.words.map((word) => word.toUpperCase());
      if (this.reversible) {
        this.directions.push({ dx: -1, dy: 0 }, { dx: 0, dy: -1 }); // Left and Up
      }

      this.words.forEach((word) => {
        let placed = false;
        for (let attempts = 0; attempts < 100; attempts++) {
          if (placed) break;
          const x = Math.floor(Math.random() * this.across);
          const y = Math.floor(Math.random() * this.down);
          const direction =
            this.directions[
              Math.floor(Math.random() * this.directions.length)
            ];
          if (this.fits(word, x, y, direction.dx, direction.dy)) {
            this.placeWord(word, x, y, direction.dx, direction.dy);
            placed = true;
          }
        }
      });

      this.fillGrid();
    },
  },
};
</script>

<style scoped>
.word-search {
  display: grid;
  grid-template-rows: repeat(auto, 1fr);
  grid-template-columns: repeat(auto, 1fr);
  border: 2px solid #000;
  margin: auto;
}
.row {
  display: flex;
}
.cell {
  display: flex;
  align-items: center;
  justify-content: center;
  border: 1px solid #000;
  background: #fff;
  text-align: center;
  font-weight: bold;
}
</style>
