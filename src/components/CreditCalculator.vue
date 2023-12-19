<template>
  <div class="calculator">
    <h2>ՎԱՐԿԱՅԻՆ ՀԱՇՎԻՉ</h2>
    <form @submit.prevent="calculateLoan">
      <div class="input-group">
        <label for="amount">Վարկի գումար</label>
        <input type="number" id="amount" v-model.number="loanAmount">
      </div>
      <div class="input-group">
        <label for="interest">Տարեկան տոկոսադրույք (%)</label>
        <input type="number" id="interest" v-model.number="interestRate">
      </div>
      <div class="input-group">
        <label for="months">Վարկի ժամկետը (ամիսներով)</label>
        <input type="number" id="months" v-model.number="loanMonths">
      </div>
      <div class="input-group">
        <label for="commission">Միանգամյա միջնորդավճար (դրամ)</label>
        <input type="number" id="commission" v-model.number="oneCommission">
      </div>
      <div class="input-group">
        <label for="commission">Ամսական միջնորդավճար (դրամ)</label>
        <input type="number" id="commission" v-model.number="monthlyCommission">
      </div>
      <button type="submit">Հաշվել</button>
    </form>
    <div v-if="resultsCalculated">
      <div class="result">
        Ավել վճարվող գումար` <span>{{ totalOverpay }} դրամ</span>
      </div>
      <div class="result">
        Փաստացի տոկոսադրույք (տարեկան)` <span>{{ overpayPercent.toFixed(2) }}%</span>
      </div>
      <div class="result">
        Ընդհանուր վճարվող գումար` <span>{{ finalAmount }} դրամ</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      loanAmount: '',
      interestRate: '',
      loanMonths: '',
      oneCommission: '',
      monthlyCommission: '',
      totalOverpay: null,
      overpayPercent: null,
      finalAmount: null,
      resultsCalculated: false
    };
  },
  methods: {
    calculateLoan() {
      if(this.loanAmount) {
        this.finalAmount = 0
        this.totalOverpay = 0
        this.overpayPercent = 0
        const totalLoanAmount = this.loanAmount + (this.loanAmount / 100);

        const calculatedInterest = this.interestRate / 100 / 12;
        const calculatedPayments = this.loanMonths;

        const x = Math.pow(1 + calculatedInterest, calculatedPayments);
        this.monthlyPayment = (totalLoanAmount * x * calculatedInterest) / (x - 1);

        // Дополнительные расчеты
        this.totalOverpay = this.finalAmount + (this.loanAmount * this.interestRate / 100) * this.loanMonths / 12;

        if(this.oneCommission) {
          this.totalOverpay += this.oneCommission
        }
        if(this.monthlyCommission) {
          this.totalOverpay = this.totalOverpay + (this.monthlyCommission * this.loanMonths)
        }

        this.finalAmount = this.totalOverpay + this.loanAmount;
        this.overpayPercent = (this.finalAmount - this.loanAmount) * 100 / this.loanAmount  / (this.loanMonths / 12);
        this.resultsCalculated = true;
      }
    },
  },
};
</script>

<style>
.calculator {
  max-width: 400px;
  margin: 20px auto;
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  background-color: #f9f9f9;
}

h2 {
  color: #333;
  font-family: 'Arial', sans-serif;
  text-align: center;
  margin-bottom: 20px;
}

.input-group {
  margin-bottom: 10px;
}

label {
  display: block;
  margin-bottom: 5px;
  color: #666;
}

input[type="number"] {
  width: 100%;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 4px;
  box-sizing: border-box;
}

button {
  display: block;
  width: 100%;
  padding: 10px;
  border: none;
  background-color: #007bff;
  color: white;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
  margin-top: 10px;
}

button:hover {
  background-color: #0056b3;
}

.result {
  margin-top: 20px;
  background-color: #e2e2e2;
  padding: 10px;
  border-radius: 4px;
  text-align: center;
}

.result span {
  font-weight: bold;
  color: #333;
}
</style>