<template>
  <q-page class="row column items-center justify-evenly">
    <div class='q-gutter-sm'>
      <enviar-artigo />
      <consultar-edital />
    </div>
  </q-page>
</template>

<script lang="ts">
import EnviarArtigo from 'components/EnviarArtigo.vue';
import ConsultarEdital from 'components/ConsultarEdital.vue';
import { Options, Vue } from 'vue-class-component';

@Options({
  components: { EnviarArtigo, ConsultarEdital }
})
export default class PageIndex extends Vue {

};
</script>
