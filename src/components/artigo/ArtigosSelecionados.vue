<template>
  <div class='q-px-lg q-pb-md'>
    <q-timeline color='secondary'>
      <q-timeline-entry heading>
        <span class='text-h5 text-bold'>Artigos selecionados</span>
      </q-timeline-entry>

      <q-timeline-entry v-for='(artigo, index) in artigos' :key='index'>
        <template v-slot:title>
          {{ artigo.title }}
        </template>
        <template v-slot:subtitle>
          {{ artigo.author }}
        </template>

        <div class='q-gutter-md'>
          <p>
            {{ artigo.abstract }}
          </p>
          <div>
            <q-btn
              label='Baixar'
              color='primary'
              icon='file_download'
              @click='onDownload(artigo)'
              outline
            />
          </div>
        </div>
      </q-timeline-entry>
    </q-timeline>
  </div>
</template>

<script lang='ts'>
import { Options, prop, Vue } from 'vue-class-component';
import { Artigo } from '../../models';

class Props {
  readonly artigos = prop<Artigo[]>({ default: [] });
}

@Options({
  components: {},
})
export default class ArtigosSelecionados extends Vue.with(Props) {
  onDownload(artigo: Artigo) {
    window.open(artigo.fileUrl, '_blank');
  }
}
</script>

<style scoped lang='sass'>

</style>
