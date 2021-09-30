<template>
  <q-page class="row items-center justify-evenly">
    <enviar-artigo />
  </q-page>
</template>

<script lang="ts">
import EnviarArtigo from 'components/EnviarArtigo.vue';
import { Options, Vue } from 'vue-class-component';

@Options({
  components: { EnviarArtigo }
})
export default class PageIndex extends Vue {

};
</script>
