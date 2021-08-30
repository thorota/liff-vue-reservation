<template>
  <div class="liff-data">
    <table>
      <tr>
        <th>OS</th>
        <td>{{ os }}</td>
      </tr>
      <tr>
        <th>Language</th>
        <td>{{ language }}</td>
      </tr>
      <tr>
        <th>LIFF SDK Version</th>
        <td>{{ sdkVersion }}</td>
      </tr>
      <tr>
        <th>LINE Version</th>
        <td>{{ lineVersion }}</td>
      </tr>
      <tr>
        <th>isInClient</th>
        <td>{{ isInClient }}</td>
      </tr>
      <tr>
        <th>isLoggedIn</th>
        <td>{{ isLoggedIn }}</td>
      </tr>
    </table>
  </div>
</template>
<template>
  <div class="profile">
    <table>
      <tr>
        <th>IDトークンの生成URL</th>
        <td>{{ token.iss }}</td>
      </tr>
      <tr>
        <th>ユーザーID</th>
        <td>{{ token.sub }}</td>
      </tr>
      <tr>
        <th>チャネルID</th>
        <td>{{ token.aud }}</td>
      </tr>
      <tr>
        <th>トークンの有効期限</th>
        <td>{{ token.exp }}</td>
      </tr>
      <tr>
        <th>IDトークンの生成時間</th>
        <td>{{ token.iat }}</td>
      </tr>
      <tr>
        <th>ユーザー認証時間</th>
        <td>{{ token.auth_time }}</td>
      </tr>
      <tr>
        <th>nonce</th>
        <td>{{ token.nonce }}</td>
      </tr>
      <tr>
        <th>認証方法</th>
        <td>{{ token.amr }}</td>
      </tr>
      <tr>
        <th>表示名</th>
        <td>{{ token.name }}</td>
      </tr>
      <tr>
        <th>プロフィールの画像URL</th>
        <td>{{ token.picture }}</td>
      </tr>
      <tr>
        <th>メールアドレス</th>
        <td>{{ token.email }}</td>
      </tr>
    </table>
  </div>
</template>

<script>
import { Component, Vue } from "vue-property-decorator";

@Component
export default class HelloWorld extends Vue {
  get os() {
    return liff.getOS();
  }

  get language() {
    return liff.getLanguage();
  }

  get lineVersion() {
    return liff.getLineVersion();
  }

  get sdkVersion() {
    return liff.getVersion();
  }

  get isInClient() {
    return liff.isInClient();
  }

  get isLoggedIn() {
    return liff.isLoggedIn();
  }

  get token() {
    return liff.getDecodedIDToken();
  }
}
</script>
