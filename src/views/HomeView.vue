<script>
import Loader from "../components/Loader.vue";
import Web3 from "web3";
import abi from "../../abi.json";
import TransferToken from "../components/TransferToken.vue";

export default {
  components: { Loader, TransferToken },
  data() {
    return {
      web3: null,
      contract: null,
      loadingContract: false,
      transferring: false,
      message: "",
      contractAddress: "0x86c12a724340f3f4f6142789808874d0a55bd01f",
    };
  },
  async mounted() {
    this.web3 = new Web3(Web3.givenProvider);
    await window.ethereum.enable();
    this.loadContract();
  },

  methods: {
    async loadContract() {
      this.loadingContract = true;
      try {
        this.contract = await new this.web3.eth.Contract(
          abi,
          this.contractAddress
        );
      } catch (e) {
        console.log(e);
        this.error = "unable to load contract";
      }
      this.loadingContract = false;
    },

    async transfer({ from, to, value }) {
      this.transferring = true;
      try {
        await this.contract.methods.transfer(to, value).send({
          from: from,
          gas: 30000,
          gasPrice: 30000,
        });
        this.message = "Your transaction is being processed";
      } catch (e) {}

      this.transferring = false;
    },
  },
};
</script>

<template>
  <main>
    <div class="title">Perform Transfer</div>
    <div class="content">
      <transfer-token @continue="transfer" />
      <template v-if="loadingContract || transferring">
        <div class="loader">
          <Loader />
        </div>
      </template>
      <p>{{ message }}</p>
    </div>
  </main>
</template>

<style scoped>
main {
  height: 500px;
  width: 40%;
  margin: auto;
  background-color: white;
  border-radius: 10px;
  padding: 20px;
}

.loader {
  display: flex;
  align-items: center;
  margin-top: 40px;
}

.title {
  height: 40px;
  color: #323643;
  font-weight: 700;
  font-size: 20px;
  text-align: center;
}
p {
  color: black;
  margin-top: 15px;
}

.content {
  height: calc(100% - 40px);
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}
</style>
