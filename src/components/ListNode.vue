<template>
  <li 
    :class="[fileType, isOpen ? 'open' : '']" 
    class="node-item" 
  >
    <a v-if="isLink" :href="file.target" @click="highlightFile">{{ file.name }}</a>
    <div v-else v-on='isDirectory ? { click: toggleDirectory } : { click: highlightFile }'>{{ file.name }}</div>

    <ul 
      v-show="isOpen" 
      v-if="isDirectory" 
      class="dirlist"
    >
      <list-node
        v-for="(subFile, index) in file.contents"
        v-bind:file="subFile"
        v-bind:key="index"
      ></list-node>
    </ul>
  </li>
</template>

<script>


// type File = {
//     type: 'file',
//     name: string,
// };

// type Link = {
//     type: 'link',
//     name: string,
//     target: string,
// };

// type Directory = {
//     type: 'directory',
//     name: string,
//     contents: Item[],4
// };

// type Item = Directory | File | Link;

export default {
  name: 'ListNode',
  props: {
    file: {
      type: Object,
    },
  },
  data: () => {
    return {
      isOpen: false,
      highlighted: false,
    }
  },
  methods: {
    toggleDirectory() {
      this.isOpen = !this.isOpen;
    },
    highlightFile(ev) {
      ev.target.classList.toggle('highlight');
      this.higlighted = !this.highlighted;
    }
  },
  computed:{
    isDirectory: function () {
      return this.file.type === 'directory'
      },
    isLink: function () {
      return this.file.type === 'link'
    },
    fileType: function () {
      return this.file.type;
    },
  }, 
}
</script>


<style scoped>
  .node-item {
    cursor: pointer;
    font-size: 1.1rem;
    padding-bottom: 0.3rem;
    padding-top: 0.3rem;
    padding-right: 0.3rem;
    padding-left: 0.3rem;
    width: fit-content;
    transition: all 0.2s ease;
  }
  .directory{
   list-style-image: url('../../public/static/icons/dir_closed.svg');
  }
  .open {
    list-style-image: url('../../public/static/icons/dir_open.svg');
  }
  .file {
    list-style-image: url('../../public/static/icons/file_icon.svg');   
  }
  .link {
    list-style-image: url('../../public/static/icons/link_icon.svg');
    color: blue;
    text-decoration: underline;
  }
  .highlight{
    color: white;
    padding-right: 0.3rem;
    padding-left: 0.3rem;
    background-color: #8390FA;
  }
  .dirlist {
    padding-left: 1.5rem;
  }
</style>
