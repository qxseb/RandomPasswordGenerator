<template>
  <div class="passwordText">
    <h3>Password Generated: {{ password }}</h3>
    <!-- <input
      class="text_input"
      v-model="password"
      placeholder="Click the button to generate password"
    /> -->

    <div class="setting">
      <select v-model="passLength" id="passLength">
        <option v-for="value in passLengthChoices" :key="value">
          {{ value }}
        </option>
      </select>
      <label for="passLength"> Password Length</label>
    </div>

    <div class="setting">
      <input
        type="checkbox"
        id="jack"
        value="numbers"
        v-model="selectedFunctions"
      />
      <label for="jack"> Allow Numbers (0-9)</label>
    </div>
    <div class="setting">
      <input
        type="checkbox"
        id="john"
        value="uppercase"
        v-model="selectedFunctions"
      />
      <label for="john"> Allow Uppercase (ABC)</label>
    </div>
    <div class="setting">
      <input
        type="checkbox"
        id="mike"
        value="lowercase"
        v-model="selectedFunctions"
      />
      <label for="mike"> Allow Lowercase (abc)</label>
    </div>
    <div class="setting">
      <input
        type="checkbox"
        id="mike"
        value="symbols"
        v-model="selectedFunctions"
      />
      <label for="mike"> Allow Symbols (!@#$%^&*()+)</label>
    </div>

    <button @click="onClick">Generate</button>
  </div>
</template>

<script>
const possibleChoices = {
  numbers: "1234567890",
  uppercase: "ABCDEFGHIJKLMNOPQRSTUVWXYZ",
  lowercase: "abcdefghijklmnopqrstuvwxyz",
  symbols: "!@#$%^&*()+",
};

export default {
  data() {
    return {
      password: "",
      selectedFunctions: ["numbers", "uppercase", "lowercase", "symbols"],
      selectedChoices: "",
      passLength: 16,
      passLengthChoices: [
        "6",
        "7",
        "8",
        "9",
        "10",
        "11",
        "12",
        "13",
        "14",
        "15",
        "16",
        "17",
        "18",
        "19",
        "20",
        "21",
        "22",
        "23",
        "24",
        "25",
        "26",
        "27",
        "28",
        "29",
        "30",
        "31",
        "32",
      ],
      onClick: () => {
        this.handleFunctions();
      },
    };
  },
  methods: {
    handleFunctions() {
      this.selectedChoices = "";
      this.selectedFunctions.forEach((func) => {
        this.selectedChoices.length < 1
          ? (this.selectedChoices = possibleChoices[func])
          : (this.selectedChoices += possibleChoices[func]);
      });
      this.selectedChoices = this.selectedChoices.split("");

      this.selectedChoices.length < 1
        ? (this.password = "No Available Chars")
        : {};

      this.loopThrough();
    },
    loopThrough() {
      let tempPass = "";
      while (tempPass.length < this.passLength) {
        const randomNumber = Math.floor(
          Math.random() * this.selectedChoices.length
        );
        tempPass += this.selectedChoices[randomNumber];
      }

      this.password = tempPass;
    },
  },
};
</script>

<style>
.passwordText {
  margin-top: 1rem;
  margin-left: 1.5rem;
}
</style>
