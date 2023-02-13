<template>
  <h2>This is my codemirror practice with Vue.js</h2>
  <codemirror
    v-model="code"
    id="editor"
    placeholder="Code goes here..."
    :style="{ height: '400px' }"
    :autofocus="true"
    :indent-with-tab="true"
    :tab-size="2"
    :extensions="extensions"
    @ready="handleReady"
    @change="log('change', $event)"
    @focus="log('focus', $event)"
    @blur="log('blur', $event)"
  />
</template>

<script>
import { defineComponent } from "vue";
import { Codemirror } from "vue-codemirror";
import { javascript } from "@codemirror/lang-javascript";
import { oneDark } from "@codemirror/theme-one-dark";
import { ref, shallowRef } from "vue";

export default defineComponent({
  components: {
    Codemirror,
  },
  setup() {
    const code = ref(
      `console.log('Hello, world!'); \nlet editorContent: 'This is content;'`
    );
    const extensions = [javascript(), oneDark];
    // Codemirror EditorView instance ref
    const view = shallowRef();
    const handleReady = (payload) => {
      view.value = payload.view;
    };

    // Status is available at all times via Codemirror EditorView
    const getCodemirrorStates = () => {
      // const state = view.value.state;
      // const ranges = state.selection.ranges;
      // const selected = ranges.reduce(
      //   (r, range) => r + range.to - range.from,
      //   0
      // );
      // const cursor = ranges[0].anchor;
      // const length = state.doc.length;
      // const lines = state.doc.lines;
    };

    return {
      code,
      extensions,
      handleReady,
      log: console.log,
      getCodemirrorStates,
    };
  },
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
#editor {
  width: 40%;
}
.cm-editor {
  width: 40%;
}
</style>
