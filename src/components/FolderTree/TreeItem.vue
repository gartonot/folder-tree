<template>
  <div>
    <div class="tree-item" @click="folderToggle(item.id)">
      <folder-open-icon v-show="isOpen" :width="iconSizePx" />
      <folder-close-icon v-show="!isOpen" :width="iconSizePx" />
      {{ item.name }}
    </div>
    <div v-show="isOpen" class="tree-children">
      <tree-item
        v-for="itemChildren in item.children"
        :item="itemChildren"
        :key="itemChildren.id"
        :event-bus="eventBus"
      />
    </div>
  </div>
</template>

<script>
  import FolderOpenIcon from '@/components/iconsComponents/FolderOpenIcon.vue'
  import FolderCloseIcon from '@/components/iconsComponents/FolderCloseIcon.vue'
  import TreeItem from '@/components/FolderTree/TreeItem.vue'

  export default {
    name: 'TreeItem',
    components: {
      FolderOpenIcon,
      FolderCloseIcon,
      TreeItem
    },
    props: {
      item: {
        type: Object,
        required: true
      },
      eventBus: {
        type: Object,
        required: true
      }
    },
    data() {
      return {
        iconSizePx: 28,
        isOpen: false
      }
    },
    computed: {
      isFolder() {
        return this.item.children && this.item.children.length
      }
    },
    methods: {
      folderToggle(id) {
        this.eventBus.$emit('select', id)
        if(this.isFolder) {
          this.isOpen = !this.isOpen
        }
      }
    }
  }
</script>

<style lang="scss" scoped>
  .tree-item {
    display: flex;
    align-items: center;
    gap: 4px;
    cursor: pointer;
  }
  .tree-children {
    margin-left: 20px;
  }
</style>
