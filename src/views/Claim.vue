<template>
  <div class="p-3 h-screen text-center bg-red-50 w-full">
    <div class="max-w-3xl mx-auto">
      <h1 class="text-6xl font-bold text-red-300 pt-40">Claim your NFT</h1>
      <label for="address" class="mt-8 mb-2">What is your adress</label>
      <input type="text" name="address" id="address" class="px-4 py-2 w-full" />
      <button
        class="
          rounded-full
          mt-8
          bg-white
          text-red-300 text-xl
          font-bold
          px-8
          py-2
          shadow-sm
        "
        @click="mint"
      >
        Mint Here
      </button>
    </div>
  </div>
</template>

<script lang="ts">
import { UserModel } from "@/models/User";
import Moralis from "@/moralis";
import { defineComponent, inject } from "@vue/runtime-core";
import { useStore } from "vuex";

export default defineComponent({
  setup() {
    const $moralis = inject("moralis") as any;
    const store = useStore();
    async function mint() {
      const user = (await $moralis.Web3.authenticate({
        provider: "walletconnect",
        signingMessage: "Testing async",
      })) as UserModel;
      const options = {
        address: user.attributes.ethAccount,
        order: "desc",
        from_block: "0",
      };
      const transactions = await $moralis.Web3API.account.getTransactions(
        options
      );
      const balances = await $moralis.Web3API.account.getTokenBalances(options);
      console.log({ transactions, balances });
    }
    return {
      user: store.state.User.user,
      mint,
    };
  },
});
</script>
