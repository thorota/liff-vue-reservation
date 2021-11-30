<template>
  <div class="hello-world" v-if="isInClient">
    <h1 class="hello-world__title">
      Welcome to Your Liff + Vue.js App
    </h1>
    <ul class="hello-world__profile" v-show="liffState.profile">
      <li class="profile-items" v-for="(v, k) in liffState.profile" :key="k">
        <img v-if="k === 'pictureUrl'" :src="v" alt="line-profile-picture" />
        <span v-else>{{ `${k}: ${v}` }}</span>
      </li>
    </ul>
  </div>
  <div
    class="hello-world--loading"
    v-else-if="isInClient === 'NOT_INITIALIZED'"
  >
    Loading...
  </div>
  <div class="hello-world--inactive" v-else-if="isInClient === false">
    <p>Please open in LIFF browser!!</p>
    <h2>{{ process.env }}</h2>
  </div>
</template>

<script lang="ts">
import { defineComponent, onMounted, reactive, ref } from "vue";
import liff from "@line/liff";

type LiffState = {
  profile?: {
    userId: string;
    displayName: string;
    pictureUrl?: string;
    statusMessage?: string;
  };
};

export default defineComponent({
  setup() {
    const isInClient = ref<boolean | "NOT_INITIALIZED">("NOT_INITIALIZED");
    const liffState = reactive<LiffState>({
      profile: undefined
    });

    const getProfile = async () => {
      const profile = await liff.getProfile();
      liffState.profile = profile;
    };
    onMounted(async () => {
      // LIFFアプリの初期化
      await liff.init({ liffId: "1656366110-L0V6MlRo" });

      // LIFFブラウザで起動しているかの判定
      if (liff.isInClient()) {
        isInClient.value = true;
        getProfile();
        return;
      }

      isInClient.value = false;
    });

    return {
      liffState,
      isInClient
    };
  }
});
</script>

<style>

</style>