<template>
  <q-layout view="lHh Lpr lFf">
    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component';
import HeaderLogo from 'components/header/HeaderLogo.vue';

@Options({
  components: {
    HeaderLogo,
  }
})
export default class MainLayout extends Vue {

}
</script>
