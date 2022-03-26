<template>
  <form @submit.prevent="$emit('continue', { from, to, value })">
    <div>
      <label>From</label>
      <br />
      <input type="text" placeholder="Enter Contract Address" v-model="from" />
    </div>
    <div>
      <label>To</label>
      <br />
      <input type="text" placeholder="Enter Contract Address" v-model="to" />
    </div>
    <div>
      <label>Value</label>
      <br />
      <input type="text" placeholder="Enter amount" v-model="value" />
    </div>

    <div>
      <button>Submit</button>
    </div>
  </form>
</template>

<script>
export default {
  data() {
    return {
      from: "",
      to: "",
      value: "",
    };
  },
};
</script>

<style scoped>
form {
  width: 100%;
  display: grid;
  grid-gap: 20px;
}

input {
  height: 50px;
  border-radius: 10px;
}

label {
  font-size: 14px;
  color: #1d1e2c;
}

input,
textarea {
  width: 100%;
  border-color: #30324b;
  border-width: 1px;
  margin-top: 5px;
  padding: 20px;
}

input:focus,
textarea:focus {
  border-color: #006156;
  border-width: 1px;
  outline: none !important;
}

textarea {
  border-radius: 10px;
  height: 200px;
}

button {
  width: 100%;
  height: 50px;
  background-color: #006156;
  border: none;
  border-radius: 10px;
  font-size: 15px;
  color: white;
  cursor: pointer;
}
</style>
