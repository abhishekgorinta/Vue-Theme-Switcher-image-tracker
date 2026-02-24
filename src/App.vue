<template>
  <div :class="['dashboard', theme]">

    <button @click="toggleTheme" :class="['btn', theme]">
      <i :class="theme === 'light'
        ? 'fa-solid fa-moon'
        : 'fa-solid fa-sun'" class="icon"></i>
      {{ theme === 'light' ? 'Dark Mode' : 'Light Mode' }}
    </button>

    <div class="container">

      <div class="card ">
        <h3>Live Input and Output</h3>
        <p class="output">{{ inputText }}</p>
        <input type="text" placeholder="Type something..." v-model="inputText" />
      </div>

      <div class="bottom">

        <div class="card">
          <h3>Activity Counter</h3>

          <div class="card">
            <h2>Theme changed:</h2>
            <h1><strong>{{ themeCount }}</strong> times</h1>
          </div>
          <br>

          <div class="card">
            <h2>Image changed: </h2>
            <h1><strong>{{ imageCount }}</strong> times</h1>
          </div>

        </div>

        <div class="card img-card">
          <h3>Image Switcher</h3>
          <img :src="currentImage" alt="image" />
          <button @click="changeImage">Change Image</button>
        </div>

      </div>
    </div> 
  </div>
</template>

<script>
export default {
  name: "Dashboard",
  data() {
    return {
      inputText: "",
      theme: "light",
      themeCount: 0,
      imageCount: 0,
      currentIndex: 0,
      images: [
        "https://picsum.photos/300/200?random=1",
        "https://picsum.photos/300/200?random=2",
        "https://picsum.photos/300/200?random=3"
      ]
    };
  },
  computed: {
    currentImage() {
      return this.images[this.currentIndex];
    }
  },
  methods: {
    toggleTheme() {
      this.theme = this.theme === "light" ? "dark" : "light";
      this.themeCount++;
    },
    changeImage() {
      this.currentIndex =
        (this.currentIndex + 1) % this.images.length;
      this.imageCount++;
    }
  }
};
</script>

<style scoped>
.dashboard {
  min-height: 100vh;
  padding: 30px;
  font-family: "Segoe UI", sans-serif;
}


.dashboard.light {
  background: #f4f6f8;
  color: #222;
}

.dashboard.dark {
  background: #1e1e2f;
  color: #f4f4f4;
}

.btn {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  padding: 10px 16px;
  border-radius: 10px;
  border: none;
  font-weight: 600;
  cursor: pointer;
}

.btn.light {
  background-color: #1f2937;
  color: #ffffff;
}

.btn.dark {
  background-color: #ffffff;
  color: #1e1e2f;
}

.btn.light .icon {
  color: #ffffff;
}

.btn.dark .icon {
  color: #1e1e2f;
}

.btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 15px rgba(0, 0, 0, 0.2);
}

.output {
  color:#4caf50;
  font-weight: 500;
  width: 100%;
  word-wrap: break-word;
  overflow-wrap: break-word;
  white-space: normal;
  line-height: 1.5;
}

.bottom {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 20px;
}

.title {
  text-align: center;
  margin-bottom: 30px;
}

.container {
  display: grid;
  grid-template-columns: repeat(1, 1fr);
  gap: 20px;
  margin-top: 10px;
}

h1,
h2 {
  text-align: center;
}

.card {
  background: inherit;
  border-radius: 12px;
  padding: 20px;
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.3);
  border: 2px solid rgba(255, 255, 255, 0.1);
  box-sizing: border-box;
  overflow: hidden;
}

.card h3 {
  margin-bottom: 15px;
}

input {
  width: 100%;
  padding: 10px 5px;
  border-radius: 6px;
  border: none;
  outline: none;
  margin-bottom: 10px;
  box-sizing: border-box;
  overflow-y: auto;

}

button {
  padding: 10px 15px;
  border-radius: 6px;
  border: none;
  cursor: pointer;
  background: #4caf50;
  color: white;
  font-weight: 600;
}

button:hover {
  opacity: 0.9;
}

.img-card img {
  width: 300px;
  border-radius: 8px;
  margin-bottom: 10px;
}

.img-card {
  display: grid;
  place-items: center;
}

@media (max-width:850px) {
  .bottom {
    display: grid;
    grid-template-columns: repeat(1, 1fr);
    gap: 20px;
  }

  .img-card img {
    width: 100%
  }
}

@media (max-width:420px) {
  .img-card img {
    width: 100%
  }

  h2 {
    font-size: 20px;
  }
}
</style>
