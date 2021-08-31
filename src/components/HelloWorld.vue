<template>
  <div class="hello-world">
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

<script>
import { Component, Vue } from "vue-property-decorator";
import liff from '@line/liff';

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
