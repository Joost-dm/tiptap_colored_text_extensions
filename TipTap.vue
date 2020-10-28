<template>
<div>
  <editor-menu-bar :editor="editor" v-slot="{ commands, isActive, getMarkAttrs }">
    <div class="menubar">
      <button
          :class="{ 'is-active': isActive.color() }"
          @click="commands.color({ color: 'orange'})"
      >
        color [ colored: {{isActive.color()}}; color: {{getMarkAttrs('color').color || "default"}} ]
      </button>
      <button
          :class="{ 'is-active': isActive.background_color() }"
          @click="commands.background_color({ color: 'orange'})"
      >
        background [ colored: {{isActive.background_color()}}; color:
        {{getMarkAttrs('background_color').color ? getMarkAttrs('background_color').color.split(' ')[0] : "default"}} ]
      </button>
    </div>
  </editor-menu-bar>
  <editor-content :editor="editor" />
</div>
</template>

<script>
import { EditorMenuBar, Editor, EditorContent } from 'tiptap'
import BackgroundColor from "@/extensions/BackgroundColor"
import Color from "@/extensions/Color"

export default {
  name: "TipTap",
  components: {
    EditorMenuBar,
    EditorContent
  },
  data() {
    return {
      editor: new Editor({
        content: '<span>This is just a boring paragraph</span>',
        extensions: [
            new Color(),
            new BackgroundColor()
        ],
      }),
    }
  },
  beforeDestroy() {
    this.editor.destroy()
  }
}
</script>
