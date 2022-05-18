<template>
  <h1> Hello Metamask </h1>
  <div v-if="!computedLoggedIn">
    <button v-if="isMetamaskSupported" @click="connectWallet">Metamask Login</button>
    <h4 v-else>Please install Metamask</h4>
  </div>
  <div v-else>
    <h1>{{ computedAddress }}</h1>
  </div>
</template>

<script>
export default {
  name: 'App',
  components: {
  },
  data() {
    return {
      msg: "This is demo network",
      isMetamaskSupported: false,
      accountAddress: '',
    }
  },
  methods: {
    async connectWallet() {
      const accounts = await window.ethereum.request({ method: 'eth_requestAccounts'});
      this.accountAddress = accounts[0];
    },
    onComplete(data) {
      console.log("data:", data);
    }
  },
  computed: {
    computedAddress() {
      return this.accountAddress.substring(0, 4) + '....';
    },
    computedLoggedIn() {
      return this.accountAddress != '';
    }
  },
  mounted() {
    this.isMetamaskSupported = typeof window.ethereum !== 'undefined';
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
