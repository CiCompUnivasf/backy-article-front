<template>
  <form @submit.prevent='submit'>
    <header-logo class='q-pb-md' />

    <q-card>
      <q-card-section class='q-gutter-md'>
        <q-input
          v-model='studentName'
          label='Nome e Sobrenome'
          required
        />
        <q-input
          v-model='email'
          label='E-mail'
          required
        />
        <q-file
          v-model='file'
          label='Artigo'
          required
          bottom-slots
          outlined
          counter
          dense
        >
          <template v-slot:prepend>
            <q-icon name='cloud_upload' @click.stop />
          </template>
          <template v-slot:append>
            <q-icon name='close' @click.stop='file = null' class='cursor-pointer' />
          </template>

          <template v-slot:hint>
            Apenas arquivos DOCX
          </template>
        </q-file>
      </q-card-section>
      <q-card-actions class='row justify-end q-pb-md q-pt-sm'>
        <q-btn label='Enviar' icon-right='send' color='amber-10' @click='submit' />
      </q-card-actions>

      <q-inner-loading :showing='loading.is'>
        <q-spinner-gears size='50px' color='primary' />
        <transition
          appear
          enter-active-class='animated fadeIn'
          leave-active-class='animated fadeOut'
        >
          <p
            v-if='loading.message'
            class='text-subtitle1 text-primary q-mt-sm'
          >
            {{ loading.message }}
          </p>
        </transition>

      </q-inner-loading>
    </q-card>
  </form>
</template>

<script lang='ts'>

import { Options, Vue } from 'vue-class-component';
import HeaderLogo from './header/HeaderLogo.vue';
import { AxiosResponse } from 'axios';

interface FileUploaded {
  message: string;
  data: {
    url: string;
  }
}

interface CreatedArticle {
  success: boolean;
  message: string;
}

interface ServerError {
  message: string | string[];
}

@Options({
  components: {
    HeaderLogo
  }
})
export default class EnviarArtigo extends Vue {
  studentName = '';

  email = '';

  file: null | File | string | Blob = null;

  loading = {
    is: false,
    message: ''
  };

  isLoading(state: boolean, message = '') {
    this.loading = {
      is: state,
      message
    };
  }

  async submit() {
    try {
      this.isLoading(true, 'Preparando arquivo para o servidor');

      const file = await this.sendFile();

      console.log('enviado', file);

      this.isLoading(true, 'Enviando artigo...')

      const article = await this.sendArticle(file.data.url);

      console.log('article', article);

      if (article.success) {
        this.$q.notify({
          message: article.message,
          type: 'positive',
          color: 'green-8',
          position: 'center',
        })
      }
    } catch (e) {
      console.error(e);
      const defaultMessage = 'Ocorreu um erro interno, avise a um membro 👍';

      let apiResponse = (e.response as AxiosResponse<ServerError>)?.data?.message;

      // ? Se for um erro vindo da API e de validação, mostrar o primeiro.
      apiResponse = Array.isArray(apiResponse) ? apiResponse[0] : apiResponse;
      const message: string = apiResponse || defaultMessage;

      // ? Não queremos exibir internal error 🤡
      if (message.toLowerCase().includes('internal server')) {
        return this.showError(defaultMessage);
      }

      this.showError(message);
    } finally {
      setTimeout(() => this.isLoading(false), 600);
    }
  }

  showError(message: string) {
    this.$q.notify({
      message,
      type: 'negative',
      color: 'red-9',
      position: 'center',
    });

    return false;
  }

  async sendFile(): Promise<FileUploaded> {
    if (this.file) {
      const formData = new FormData()
      formData.append('file', this.file);

      const { data } = await this.$api.post<FileUploaded>(
        'upload',
        formData,
        {
          headers: {
            'Content-Type': 'multipart/form-data'
          }
        });

      return data;
    }

    throw new Error('Insira um arquivo')
  }

  async sendArticle(file: string): Promise<CreatedArticle> {
    const {data} = await this.$api.post<CreatedArticle>('/', {
      studentName: this.studentName,
      mail: this.email,
      uploadedFile: file,
    })

    return data;
  }
}
</script>
