<script lang="ts" setup>
import { ref, onMounted } from "vue";
import { createPatch } from "diff";
import { ColorSchemeType } from "diff2html/lib/types";
import { Diff2HtmlUI } from "diff2html/lib/ui/js/diff2html-ui";
import "diff2html/bundles/css/diff2html.min.css";

const uiRef = ref();
const init = async () => {
  const oldJson = { name: "Tom" };
  const newJson = { name: "Jerry", age: 18 };
  const oldText = JSON.stringify(oldJson, null, 2);
  const newText = JSON.stringify(newJson, null, 2);
  const diffoutput = createPatch("", oldText, newText, "1.0.0", "1.1.1");

  const ui = new Diff2HtmlUI(uiRef.value, diffoutput, {
    drawFileList: true,
    fileListToggle: false,
    fileListStartVisible: false,
    matching: "lines",
    outputFormat: "side-by-side",
    synchronisedScroll: true,
    highlight: true,
    colorScheme: ColorSchemeType.DARK,
    renderNothingWhenEmpty: false,
  });
  ui.draw();
};
onMounted(async () => {
  init();
});
</script>
<template>
  <div ref="uiRef"></div>
</template>
