<script lang="ts">
import 'github-markdown-css'
import marked from 'marked'
import DOMPurify from 'dompurify'
import hljs, { supportedLangNames } from './highlight'

marked.setOptions({
  gfm: true,
  highlight(code: string, langName: string, callback?: (error: any, code?: string) => void): string | void {
    if (supportedLangNames.has(langName)) {
      return hljs.highlight(code, {language: langName}, true).value
    }
  }
})

export let source: string = ''

$: compiledSecureHTML = DOMPurify.sanitize(marked(source))
</script>

<article class="previewer markdown-body">
  {@html compiledSecureHTML}
</article>

<style>
.previewer {
  flex: 1;
  height: 100%;
  overflow: auto;
  word-break: break-word;
}
</style>
