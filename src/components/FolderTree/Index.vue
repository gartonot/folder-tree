<template>
  <tree-item
    class="folder-tree"
    :item="treeList"
    :event-bus="eventBus"
  />
</template>

<script>
  import TreeItem from '@/components/FolderTree/TreeItem.vue'

  export default {
    name: 'FolderTree',
    components: {
      TreeItem
    },
    props: {
      eventBus: {
        type: Object,
        required: true
      }
    },
    data() {
      return {
        treeList: {
          id: 0,
          name: 'folder-tree',
          children: [
            { id: 1, name: 'node_modules' },
            { id: 2, name: 'public' },
            {
              id: 3,
              name: 'src',
              children: [
                {
                  id: 4,
                  name: 'assets',
                  children: [
                    { id: 5, name: 'scss' }
                  ]
                },
                {
                  id: 6,
                  name: 'components',
                  children: [
                    { id: 7, name: 'FolderTree' },
                    { id: 8, name: 'iconsComponents' },
                    { id: 9, name: 'ui' },
                  ]
                },
              ]
            },
          ]
        }
      }
    }
  }
</script>

<style lang="scss" scoped>
  .folder-tree {
    padding: 12px;
  }
</style>
