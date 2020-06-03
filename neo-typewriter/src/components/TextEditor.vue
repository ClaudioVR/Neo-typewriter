<template>
  <div>

    <div class="editor">
      <v-row>
        <v-col class="d-flex align-end justify-space-between" cols="12" sm="10" offset-sm="1">
          <v-btn class="custom-transform-class text-none" small color="#3ab508" outlined @click="exportHTML">Download as .doc</v-btn>
          <editor-menu-bar :editor="editor" v-slot="{ commands, isActive }">
            <div class="menubar text-right">

              <button
                class="menubar__button"
                :class="{ 'is-active': isActive.bold() }"
                @click="commands.bold"
              >
                <v-icon color="#3ab508">mdi-format-bold</v-icon>
              </button>

              <button
                class="menubar__button"
                :class="{ 'is-active': isActive.italic() }"
                @click="commands.italic"
              >
                <v-icon color="#3ab508">mdi-format-italic</v-icon>
              </button>

              <button
                class="menubar__button"
                :class="{ 'is-active': isActive.underline() }"
                @click="commands.underline"
              >
                <v-icon color="#3ab508">mdi-format-underline</v-icon>
              </button>

              <button
                class="menubar__button"
                :class="{ 'is-active': isActive.code() }"
                @click="commands.code"
              >
                <v-icon color="#3ab508">mdi-code-tags</v-icon>
              </button>

              <button
                class="menubar__button"
                :class="{ 'is-active': isActive.paragraph() }"
                @click="commands.paragraph"
              >
                <v-icon color="#3ab508">mdi-format-paragraph</v-icon>
              </button>

              <button
                class="mx-1 menubar__button"
                :class="{ 'is-active': isActive.heading({ level: 1 }) }"
                @click="commands.heading({ level: 1 })"
              >
                <span class="font-weight-bold">H1</span>
              </button>

              <button
                class="mx-1 menubar__button"
                :class="{ 'is-active': isActive.heading({ level: 2 }) }"
                @click="commands.heading({ level: 2 })"
              >
                <span class="font-weight-bold">H2</span>
              </button>

              <button
                class="mx-1 menubar__button"
                :class="{ 'is-active': isActive.heading({ level: 3 }) }"
                @click="commands.heading({ level: 3 })"
              >
                <span class="font-weight-bold">H3</span>
              </button>

              <button
                class="menubar__button"
                :class="{ 'is-active': isActive.bullet_list() }"
                @click="commands.bullet_list"
              >
                <v-icon color="#3ab508">mdi-format-list-bulleted</v-icon>
              </button>

              <button
                class="mx-1 menubar__button"
                :class="{ 'is-active': isActive.code_block() }"
                @click="commands.code_block"
              >
                <v-icon color="#3ab508">mdi-code-tags</v-icon>
              </button>

              <button
                class="mx-1 menubar__button"
                @click="commands.horizontal_rule"
              >
                <span>-</span>
              </button>

              <button
                class="ml-5 menubar__button"
                @click="commands.undo"
              >
                <v-icon color="#3ab508">mdi-undo</v-icon>
              </button>

              <button
                class="menubar__button"
                @click="commands.redo"
              >
                <v-icon color="#3ab508">mdi-redo</v-icon>
              </button>

            </div>
          </editor-menu-bar>
        </v-col>
        <v-col cols="12" sm="10" offset-sm="1">
          <editor-content class="mt-n2 editor__content" :editor="editor" />
          <div class="actions">
            <button class="button" @click="clearContent">
              Clear Content
            </button>
          </div>
        </v-col>
      </v-row>

    </div>



  </div>
</template>

<script>
import { Editor, EditorContent, EditorMenuBar } from 'tiptap'
import {
  Blockquote,
  CodeBlock,
  HardBreak,
  Heading,
  HorizontalRule,
  OrderedList,
  BulletList,
  ListItem,
  TodoItem,
  TodoList,
  Bold,
  Code,
  Italic,
  Link,
  Strike,
  Underline,
  History,
} from 'tiptap-extensions'
export default {
  components: {
    EditorContent,
    EditorMenuBar,
  },
  data() {
    return {
      editor: new Editor({
        extensions: [
          new Blockquote(),
          new BulletList(),
          new CodeBlock(),
          new HardBreak(),
          new Heading({ levels: [1, 2, 3] }),
          new HorizontalRule(),
          new ListItem(),
          new OrderedList(),
          new TodoItem(),
          new TodoList(),
          new Link(),
          new Bold(),
          new Code(),
          new Italic(),
          new Strike(),
          new Underline(),
          new History(),
        ],
        content: `
          <p>
            Wake up, Neo...
          </p>
          <p>
            It's time to start your novel.
          </p>
        `,
        onUpdate: ({ getJSON, getHTML }) => {
          this.json = getJSON()
          this.html = getHTML()
        },
      }),
      json: 'Update content to see changes',
      html: 'Update content to see changes',
    }
  },
  methods: {
    exportHTML(){
        var header = "<html xmlns:o='urn:schemas-microsoft-com:office:office' "+
             "xmlns:w='urn:schemas-microsoft-com:office:word' "+
             "xmlns='http://www.w3.org/TR/REC-html40'>"+
             "<head><meta charset='utf-8'><title>Export HTML to Word Document with JavaScript</title></head><body>";
        var footer = "</body></html>";
        var sourceHTML = `${header}${this.html}${footer}`;

        var source = 'data:application/vnd.ms-word;charset=utf-8,' + encodeURIComponent(sourceHTML);
        var fileDownload = document.createElement("a");
        document.body.appendChild(fileDownload);
        fileDownload.href = source;
        fileDownload.download = 'document.doc';
        fileDownload.click();
        document.body.removeChild(fileDownload);
     },
    clearContent() {
      this.editor.clearContent(true)
      this.editor.focus()
    },
  },
}
</script>

// <style lang="scss" scoped>
// @import "~variables";
// .actions {
//   max-width: 30rem;
//   margin: 0 auto 2rem auto;
// }
// .export {
//   max-width: 30rem;
//   margin: 0 auto 2rem auto;
//   pre {
//     padding: 1rem;
//     border-radius: 5px;
//     font-size: 0.8rem;
//     font-weight: bold;
//     background: rgba($color-black, 0.05);
//     color: rgba($color-black, 0.8);
//   }
//   code {
//     display: block;
//     white-space: pre-wrap;
//   }
// }
// </style>
