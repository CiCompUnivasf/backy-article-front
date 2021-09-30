<template>
  <q-layout view='hHh lpR fFf'>

    <q-header reveal elevated class='bg-primary text-white'>
      <q-toolbar>
        <q-toolbar-title>
          <q-avatar>
            <img src='logos/backy.png'>
          </q-avatar>
          <span>BackyArticle</span>
        </q-toolbar-title>
      </q-toolbar>
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script lang='ts'>
import { Options, Vue } from 'vue-class-component';
import HeaderLogo from 'components/header/HeaderLogo.vue';

@Options({
  components: {
    HeaderLogo
  }
})
export default class ArtigoLayout extends Vue {

}
</script>
