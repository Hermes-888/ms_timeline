<template>
  <div class="content-panel">
    <div class="panel-content"
      v-html="parseContent"
    >
    </div>
  </div>
</template>

<script>
/**
 * Display html content
 * or fetch a link 
 * if './msData || http'
 * 
 */
  export default {
    name: 'ContentPanel',
    props: {
      itemContent: {
        type: String,
        default: ''
      }
    },
    computed: {
      parseContent: function () {
        if (this.itemContent.substring(0, 10).includes('http')) {
          console.log('fetch content link');
          return this.itemContent;
        } else {
          return this.itemContent;
          // return JSON.parse(this.itemContent);
        }
      }
    }
  }
</script>
<style>
  .content-panel {
    width: 97%;
    padding: 20px;
    overflow-y: auto;
    background-color: #ffffff;
    border: 2px solid #666666;
  }
  .panel-content {
    line-height: 1.5em;
  }
</style>