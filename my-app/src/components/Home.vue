<template>
    <div>
      <div class="container">
        <div v-for="number in numbersList" :key="number" class="grid">{{ heartNumbers(number) }}</div>
      </div>

      <h1>Number Validation Form</h1>
      <!-- Display the answer rate -->
      <p v-if="answerRate !==null">Answer Rate: {{ answerRate }}%</p>

        <!-- Display an error message if the numbers don't meet the criteria -->
        <p v-if="errorMessage" style="color: red;">{{ errorMessage }}</p>
        
        <!-- Form with a table for entering numbers -->
        <form @submit.prevent="handleSubmit">
            <label for="a">❤️:</label>
            <input type="number" v-model="numbers.a" required>
            
            <label for="b">💛:</label>
            <input type="number" v-model="numbers.b" required>

            <label for="c">💙:</label>
            <input type="number" v-model="numbers.c" required>

            <label for="d">💚:</label>
            <input type="number" v-model="numbers.d" required>

            
            <!-- Submit button -->
            <button type="submit">Submit</button>
        </form>
    </div>
  </template>
  
  <script>
  export default {
    name: 'HomePage', // 改为多词命名
    data () {
        return {
            numbersList: Array.from({length:50},(_,index)=>index+1),
            numbers: {a:0, b:0, c:0, d:0}, // Initial numbers
            errorMessage: '', // Error message for number validation
            answerRate: null
        };
    },
    methods: {
        heartNumbers(number) {
            if (number===3) {
                number = "❤️";
            }

            else if (number===10) {
                number = "💛";
            }

            else if (number===21) {
                number = "💙";
            }

            else if (number===50) {
                number = "💚";
            }
            return number;
        },
        handleSubmit() {
        // Check if the numbers meet the expected criteria
            // if (this.areNumbersValid()) {
            //calculate answer rate
            const correctAnswers = this.getCorrectAnswers();
            const totalQuestions = Object.keys(this.numbers).length;
            this.answerRate = (correctAnswers/totalQuestions) *100;
            // Do something with the valid numbers (e.g., send to a server)
            console.log('Numbers are valid:', this.numbers);
            this.errorMessage = ''; // Clear any previous error message
            // }
            // } else {
            //     // Display an error message if numbers are not valid
            //     this.errorMessage = 'Numbers must be 3, 10, 21, and 50.';
            //     this.answerRate = null;
            // }
        },
        // areNumbersValid() {
        // const expectedNumbers = [3, 10, 21, 50];
        // return Object.values(this.numbers).every((number, index) => number === expectedNumbers[index]);
        // // Check if all numbers are greater than 0 and less than 100
        // // return this.numbers.every(number => number > 0 && number < 100);
        // },
        getCorrectAnswers() {
            const expectedNumbers = [3,10,21,50];
            const a  = Object.values(this.numbers).filter((number,index) => number ===expectedNumbers[index]).length;
            console.log(a);
            return Object.values(this.numbers).filter((number,index) => number ===expectedNumbers[index]).length;
        }
    }

    }
  </script>
  
  <style scoped>
  .container {
    display: grid;
    grid-template-columns: repeat(10,1fr);
    gap:10px;
    max-width: 600px;
    margin: 0 auto;

  }
    .grid {
        border: 1px solid #333;
        width: 30px;
    height: 30px;
    display: flex;
    align-items: center;
    justify-content: center;
    margin: 5px;
    }
  </style>
  