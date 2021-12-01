<template>
  <div class="hello-world" v-if="isInClient">
    <h1 class="">
      Welcome to Your Liff + Vue.js App
    </h1>
    <ul class="" v-show="liffState.profile">
      <li class="profile-items" v-for="(v, k) in liffState.profile" :key="k">
        <img v-if="k === 'pictureUrl'" :src="v" alt="line-profile-picture" />
        <span v-else>{{ `${k}: ${v}` }}</span>
      </li>
    </ul>
    <div class="field">
      <label>name</label>
      <input
        v-model="field.name"
        type="text"
        placeholder="名前を入力してください!"
      >
    </div>
    <div class="field">
      <label>tel</label>
      <input
      v-model="field.tel"
      type="text"
      placeholder="電話番号を入力してください"
      />
    </div>
    <button
      class="button"
      @click="onSendClick()"
    >
      送信
    </button>
  </div>
  <div
    class=""
    v-else-if="isInClient === 'NOT_INITIALIZED'"
  >
    Loading...
  </div>
  <div class="" v-else-if="isInClient === false">
    Please open in LIFF browser!!
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
interface Field {
  name: string,
  tel: string,
}

export default defineComponent({
  setup() {
    const isInClient = ref<boolean | "NOT_INITIALIZED">("NOT_INITIALIZED");
    const liffState = reactive<LiffState>({
      profile: undefined
    });
    const field = ref<Field>({
      name: '',
      tel: '',
    })

    const getProfile = async () => {
      const profile = await liff.getProfile();
      liffState.profile = profile;
    };
    
    const sendMessage = async () => {
      const profile = await liff.getProfile();
      liffState.profile = profile;
      liff.sendMessages([{
      'type': 'text',
      'text': field.value.name + field.value.tel
      }]).then(function() {
        window.alert('Message sent');
      }).catch(function(error) {
        window.alert('Error sending message: ' + error);
      });
    };

    const onButtonClick = () => {
      sendMessage();
    }
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