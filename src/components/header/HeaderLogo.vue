<template>
  <div class='flex flex-center'>
    <div style='width: 400px'>
      <q-img :src='logo' spinner-color='black' />
    </div>
  </div>
</template>

<script lang='ts'>
import { Options, Vue } from 'vue-class-component';

@Options({
  components: {}
})
export default class HeaderLogo extends Vue {
  public readonly logo = 'logos/logo-1.svg'
}
</script>

<style scoped lang='sass'>

</style>
