<template>
  <div class="calculator">
    <h1>Calculator</h1>
    <input
      type="text"
      class="display"
      v-model="expression"
      disabled
      @keydown="handleKeydown"
    />
    <div class="buttons">
      <button
        v-for="button in buttons"
        :key="button.label"
        class="animated-button"
        @click="handleButtonClick(button)"
      >
        {{ button.label }}
      </button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      expression: "",
      buttons: [
        { label: "⌫", value: "Backspace" },
        { label: "7", value: "7" },
        { label: "8", value: "8" },
        { label: "9", value: "9" },
        { label: "+", value: "+" },
        { label: "4", value: "4" },
        { label: "5", value: "5" },
        { label: "6", value: "6" },
        { label: "-", value: "-" },
        { label: "1", value: "1" },
        { label: "2", value: "2" },
        { label: "3", value: "3" },
        { label: "*", value: "*" },
        { label: "0", value: "0" },
        { label: ".", value: "." },
        { label: "=", value: "=" },
        { label: "/", value: "/" },
        { label: "AC", value: "AC" },
        { label: "(", value: "(" },
        { label: ")", value: ")" },
        { label: "√", value: "Math.sqrt(" },
        { label: "π", value: "Math.PI" },
        { label: "x²", value: "**2" },
        { label: "x³", value: "**3" },
      ],
    };
  },
  methods: {
    handleButtonClick(button) {
      const value = button.value;
      switch (value) {
        case "=":
          this.calculate();
          break;
        case "AC":
          this.expression = "";
          break;
        case "Backspace":
          this.expression = this.expression.slice(0, -1);
          break;
        case "Math.sqrt(":
          this.expression += "Math.sqrt(";
          break;
        case "Math.PI":
          this.expression = this.expression * Math.PI.toString();
          break;
        case "**2":
          this.expression += "**2";
          break;
        case "**3":
          this.expression += "**3";
          break;
        default:
          this.expression += value;
          break;
      }
    },

    calculate() {
      try {
        // eslint-disable-next-line no-new-func
        const result = Function(`return (${this.expression})`)();
        this.expression = result.toString();
      } catch (error) {
        this.expression = "Error";
      }
    },
    handleKeydown(event) {
      const key = event.key;
      const allowedKeys = /[0-9+\-*/.=]/;
      if (!allowedKeys.test(key) && key !== "Backspace") {
        event.preventDefault();
        return;
      }

      event.preventDefault();

      switch (value) {
        case "=":
          this.calculate();
          break;
        case "AC":
          this.expression = "";
          break;
        case "Enter":
          this.calculate();
          break;
        case "Backspace":
          this.expression = this.expression.slice(0, -1);
          break;
        default:
          this.expression += value;
          break;
      }
    },
  },
};
</script>

<style>
.calculator {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 670px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
  border-radius: 10px;
  padding: 20px;
  background-color: #e7e3e360;
  max-width: 400px;
  margin: 0 auto;
  margin-top: 5rem !important;
}
h1 {
  color: black;
  font-size: 40px;
  margin-top: -50px;
  font-weight: bold;
  text-align: center;
}

.display {
  width: 100%;
  height: 60px;
  /* padding: 10px; */
  width: 85%;
  font-size: 24px;
  text-align: right;
  margin-bottom: 20px;
  color: #ffffff;
  background-color: #ffffff;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.buttons {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 10px;
}

button {
  width: 80px;
  height: 60px;
  font-size: 24px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #3f4144b6;
}
.animated-button {
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  padding: 10px 20px;
  border: none;
  background-color: #fff;
  color: black;
  border-radius: 8px;
  cursor: pointer;
}

.animated-button:hover {
  transform: scale(1.05);
  box-shadow: 0 8px 15px rgba(0, 0, 0, 0.2);
}

@media (max-width: 480px) {
  .calculator {
    max-width: 240px;
  }

  .display {
    font-size: 20px;
    height: 50px;
  }

  button {
    font-size: 18px;
    width: 50px;
  }
}
</style>
