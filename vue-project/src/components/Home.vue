<template>

  <div>
    <h2>Bienvenido</h2>
    <input v-model="domainName">
    <button @click="getArguments">Guardar</button>
  </div>



</template>

<script setup>
import {onMounted, ref} from "vue";
import {ethers} from "ethers";
import abi from '../../../src/artifacts/contracts/Domains.sol/Domains.json'

const {ethereum} = window;
const currentAccount = ref();
const CONTRACT_ADDRESS= '0x7e4F785faf5296d1f1e9e4Ca62EF5CCb7Ed703D8';
const domainName = ref('pepito');
const CONTRACT_ABI = "../../../src/artifacts/contracts/Domains.sol/Domains.json"
const provider = new ethers.providers.Web3Provider(ethereum);
const signer = provider.getSigner();
const contract = new ethers.Contract(CONTRACT_ADDRESS, abi.abi, signer);
console.log(abi.abi, 'as555555555555555555assa')
console.log({abi})


const saveInfo = async () => {
  const operationPrice = '.0001';

  let tx = await contract.register(domainName.value,{value: ethers.utils.parseEther(operationPrice)});
  const receipt = await tx.wait();

  tx = await contract.setArgument(domainName.value, 'sdsdsdds');
  await tx.wait();

  console.log('Operation finished succefully https://mumbai.polygonscan.com/tx/' + tx.hash);
  // const record = await contract.arguments();
  // console.log({record})
}

const getArguments = async () => {
  const record = await contract.arguments();
  await record.wait();
  console.log({record})
}

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
checkIfWalletIsConnected()

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
