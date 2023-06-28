<template>
  <main class="app">
    <section class="wrapper">
      <app-button label="Открыть" @click="modalOpen()"/>
      <h1>
        Выбранная папка
        <span v-if="currentIdFolder !== null">
          [id: {{ currentIdFolder }}]
        </span>
      </h1>
    </section>
    <app-modal :is-open="isOpen" @modal-close="modalClose()">
      <template #header>
        <h2>Folder list</h2>
      </template>
      <template #default>
        <folder-tree :event-bus="eventBus" />
      </template>
    </app-modal>
  </main>
</template>

<script>
  import AppButton from '@/components/ui/AppButton.vue'
  import AppModal from '@/components/ui/AppModal.vue'
  import FolderTree from '@/components/FolderTree/Index.vue'
  import Vue from 'vue'

  export default {
    name: 'App',
    components: {
      AppButton,
      AppModal,
      FolderTree
    },
    data() {
      return {
        isOpen: false,
        currentIdFolder: null,
        eventBus: new Vue()
      }
    },
    created() {
      this.eventBus.$on('select', (id) => {
        this.currentIdFolder = id
      })
    },
    methods: {
      modalClose() {
        this.isOpen = false
      },
      modalOpen() {
        this.isOpen = true
      }
    }
  }
</script>

<style lang="scss" scoped>
  .app {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100vh;

    .wrapper {
      display: flex;
      flex-direction: column;
      gap: 20px;
    }
  }
</style>
