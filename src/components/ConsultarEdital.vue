<template>
  <div class='row'>
    <p class='text-dark'>Para ver o edital <a class='q-link text-blue-8' :href='fileUrl' target='_blank'>clique aqui</a> </p>
  </div>
</template>

<script lang='ts'>
import { Options, Vue } from 'vue-class-component';

@Options({
  components: {}
})
export default class ConsultarEdital extends Vue {
  openFile() {
    window.top.open(this.fileUrl, '_blank')
  }


  get fileUrl() {
    return 'https://ccicomp.s3.amazonaws.com/uploads/Edital_Revista_BackArticle_2021.pdf'
  }
}
</script>

<style scoped lang='sass'>

</style>
