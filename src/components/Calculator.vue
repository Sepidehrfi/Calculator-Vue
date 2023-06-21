<template>
  <div class="calculator">
  <h1>Calculator</h1>  
    <input type="text" class="display" v-model="expression" disabled @keydown="handleKeydown">
    <div class="buttons">
      <button v-for="button in buttons" :key="button.label" @click="handleButtonClick(button)">{{ button.label }}</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      expression: '',
      buttons: [
        { label: '7', value: '7' },
        { label: '8', value: '8' },
        { label: '9', value: '9' },
        { label: '+', value: '+' },
        { label: '4', value: '4' },
        { label: '5', value: '5' },
        { label: '6', value: '6' },
        { label: '-', value: '-' },
        { label: '1', value: '1' },
        { label: '2', value: '2' },
        { label: '3', value: '3' },
        { label: '*', value: '*' },
        { label: '0', value: '0' },
        { label: '.', value: '.' },
        { label: '=', value: '=' },
        { label: '/', value: '/' },
        { label: 'AC', value: 'AC' }, // AC button
      ],
    };
  },
  methods: {
handleButtonClick(button) {
  if (button.value === '=') {
    this.calculate();
  } else if (button.value === 'AC') { // Handle AC button
    this.expression = '';
  } else {
    this.expression += button.value;
  }
},


    calculate() {
      try {
        this.expression = eval(this.expression);
      } catch (error) {
        this.expression = 'Error';
      }
    },
    handleKeydown(event) {
      const key = event.key;
      const allowedKeys = /[0-9+\-*/.=]/;
      if (!allowedKeys.test(key) && key !== 'Backspace') {
        event.preventDefault();
        return;
      }

      event.preventDefault();

      switch (key) {
        case '=':
        case 'Enter':
          this.calculate();
          break;
        case 'Backspace':
          this.expression = this.expression.slice(0, -1);
          break;
        default:
          this.expression += key;
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
  height: 600px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
  border-radius: 10px;
  padding: 20px;
  background-color: #f5f5f5;
  max-width: 400px;
  margin: 0 auto;
}
h1{
  color: #34495E;
  font-size: 40px;
  margin-top: -50px;
  font-weight: bold;
  text-align: center;

}

.display {
  width: 100%;
  height: 60px;
  padding: 10px;
  font-size: 24px;
  text-align: right;
  margin-bottom: 20px;
  background-color: #fff;
  border-radius: 5px;
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
  background-color: #34495E;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #263238;
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
