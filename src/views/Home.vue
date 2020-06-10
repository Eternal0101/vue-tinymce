<template>
  <div class="home">
    <tinymce-editor ref="editor"
        v-model="content"
        :language="language"
        :skin="skin"
        @input="getInput"
    >
    </tinymce-editor>
    <!--展示用户输入的内容-->
    <div v-html="content"></div>
  </div>
</template>

<script>
import TinymceEditor from '@/components/tinymce/tinymce';
export default {
  name: 'Home',
  data(){
    return {
      language: 'zh_CN',
      skin: 'oxide',
      content:''
    }
  },
  components: {
    TinymceEditor
  },
  methods:{
    getInput(input){
      this.content = input;
    }
  }
}
</script>
