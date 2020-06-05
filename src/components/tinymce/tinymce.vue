<template>
    <div class="tinymce-editor">
        <editor v-model="editorContent"
                :init="init">
        </editor>
    </div>
</template>
<script>
    import tinymce from 'tinymce/tinymce'
    import Editor from '@tinymce/tinymce-vue'
    import 'tinymce/themes/silver/theme'
    //插件plugins
    import 'tinymce/plugins/image'// 插入上传图片插件
    import 'tinymce/plugins/table'// 插入表格插件
    import 'tinymce/plugins/lists'// 列表插件
    import "tinymce/icons/default/icons.js";
    export default {
        components: {
            Editor
        },
        props: {
            value: {
                type: String,
                default: ''
            },
            plugins: {
                type: [String, Array],
                default: 'lists image table powerpaste',
            },
            toolbar: {
                type: [String, Array],
                default: 'undo redo |  formatselect | fontsizeselect | fontselect | bold italic forecolor backcolor | alignleft aligncenter alignright alignjustify | bullist numlist outdent indent | lists image table | removeformat'
            }
        },
        data () {
            return {
                init: {
                    language_url: `/tinymce/langs/zh_CN.js`,
                    language: 'zh_CN',
                    skin_url: `/tinymce/skins/ui/oxide`,
                    content_css: `/tinymce/skins/content/default/content.css`,//${this.baseUrl}
                    height: 600,
                    plugins: this.plugins,
                    toolbar: this.toolbar,
                    fontsize_formats: "8px 10px 12px 14px 16px 18px 20px 22px 24px 26px 28px 30px 32px 34px 36px",
                    branding: false,
                    menubar: false,
                    //添加额外的插件
                    external_plugins: {
                        'powerpaste': `/tinymce/powerpaste/plugin.min.js`//${this.baseUrl}
                    },
                    powerpaste_word_import: 'merge',// 参数:propmt, merge, clear
                    powerpaste_html_import: 'merge',// propmt, merge, clear
                    powerpaste_allow_local_images: false,//粘贴图片
                    paste_data_images: false,
                    content_style: `
                        *                         { padding:0; margin:0; }
                        html, body                { height:100%; }
                        img                       { max-width:100%; display:block;height:auto; }
                        a                         { text-decoration: none; }
                        iframe                    { width: 100%; }
                        p                         { line-height:1.6; margin: 0px; }
                        table                     { word-wrap:break-word; word-break:break-all; max-width:100%; border:none; border-color:#999; }
                        .mce-object-iframe        { width:100%; box-sizing:border-box; margin:0; padding:0; }
                        ul,ol                     { list-style-position:inside; }
                      `,
                    // 图片上传配置
                    images_upload_handler: function (blobInfo, success, failure){
                        let formData = new FormData();
                        formData.append('file',blobInfo.blob());
                        formData.append('articleType',1);
                        formData.append('attachmetType',3);
                    },
                },
                editorContent: this.value
            }
        },
        mounted () {
            //tinymce.init({});
        },
        methods: {

        },
        watch: {
            value (newValue) {
                this.editorContent = newValue;
            },
            myValue (newValue) {
                this.$emit('input', newValue);
            }
        }
    }

</script>
<style>
    .tox .tox-notification--error{
        transition: opacity 1s ease-out;
    }
    .tox .tox-notification{
        transition: opacity 1s ease-out !important;
    }
    .tox .tox-notification--in{
        opacity: 0!important;
    }
</style>