<template>
  <Suspense>
    <template #default>
      <h2>Bienvenido</h2>
    </template>
  </Suspense>


</template>

<script setup>
import {onMounted, ref} from "vue";

const {ethereum} = window;
const currentAccount = ref();

onMounted( () => {
  checkIfWalletIsConnected();

})


const checkIfWalletIsConnected = () => {
  if (!ethereum) {
    console.log('ERROR IN CONNECTING TO WALLET');
  } else {
    console.log('isConected')
  }
}
console.log({ethereum})
const accounts = await ethereum.request({ method: "eth_accounts" });
console.log(accounts)
if (accounts.length !== 0) {
  currentAccount.value = accounts[0];
} else {
  console.log('No hay cuentas authorizadas');
  console.log('Autorizando....');
  accounts.value = await ethereum.request({method: 'eth_requestAccounts'});
}
</script>
<style scoped>

</style>
