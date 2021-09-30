<template>
 <section class='q-ma-lg'>
   <q-card class='q-pa-lg'>
     <q-card-section class='row q-gutter-md'>
       <div class='flex column justify-center q-gutter-sm' style='width: 200px'>
         <q-img :src='thumb' />
         <q-btn label='Baixar edição' icon='file_download' color='dark' @click='onDownload' outline />
       </div>
       <div class='q-gutter-md'>
         <p class='text-h5 text-center'>{{ title }}</p>
         <p class='text-dark'>Publicado em <span>30/09/2021</span></p>

         <p class='text-subtitle1 text-bold'>Autores</p>

          <div class='q-gutter-xs'>
            <p v-for='(autor, i) in autores' :key='i'>
              - {{ autor }}
            </p>
          </div>
       </div>
     </q-card-section>
     <q-card-section>
       <q-separator />
       <artigos-selecionados :artigos='artigos' />
     </q-card-section>
   </q-card>
 </section>
</template>

<script lang='ts'>
import { Options, Vue } from 'vue-class-component';
import ArtigosSelecionados from '../components/artigo/ArtigosSelecionados.vue';
import { Artigo } from '../models';

@Options({
  components: {
    ArtigosSelecionados,
  }
})
export default class VisualizarArtigo extends Vue {
  artigos: Artigo[] = [
    {
      title: 'Titulo qualquer sobre alguma coisa',
      author: 'Jeffyter Saraiva',
      abstract: 'abstract...',
      fileUrl: 'https://ccicomp.s3.amazonaws.com/uploads/Edital_Revista_BackArticle_2021.pdf',
    },
    {
      title: 'Titulo de um artigo qualquer',
      author: 'Melk Monteiro',
      abstract: 'abstract...',
      fileUrl: 'https://ccicomp.s3.amazonaws.com/uploads/Edital_Revista_BackArticle_2021.pdf',
    },
  ];

  title = 'v. 11 n. 25 (2021): Edição Regular e Dossiê – Educação, Saúde e Direitos Humanos / Dossiê - O campo da História da Educacão No Brasil'
  thumb = 'https://www.periodicos.univasf.edu.br/public/journals/1/cover_issue_57_pt_BR.jpg';
  url = 'https://www.periodicos.univasf.edu.br/index.php/revasf/issue/view/57/29';

  onDownload() {
    window.open(this.url, '_blank');
  }

  get autores() {
    return this.artigos.map((artigo) => artigo.author);
  }
}
</script>

<style scoped lang='sass'>

</style>
