<template>
  <div class="max-w-4xl mx-auto space-y-8">
    <!-- Form Card -->
    <div class="card p-6">
      <div class="mb-6">
        <h2 class="text-xl font-semibold text-gray-900 dark:text-white mb-2">Send a Message</h2>
        <p class="text-dimmed">Share your thoughts with the community</p>
      </div>
      
      <form @submit.prevent="handleSubmit" class="space-y-6">
        <div>
          <label for="name" class="block text-sm font-medium text-gray-900 dark:text-white mb-2">
            Your Name
          </label>
          <input
            id="name"
            v-model="formData.name"
            type="text"
            required
            :disabled="loading"
            class="input-field"
            placeholder="Enter your name"
          />
        </div>
        
        <div v-if="error" class="card border-l-4 border-l-red-500 bg-red-50/50 dark:bg-red-500/10 p-4">
          <div class="flex items-start">
            <div class="w-8 h-8 bg-red-100 dark:bg-red-500/20 rounded-full flex items-center justify-center flex-shrink-0">
              <svg class="w-4 h-4 text-red-500" fill="currentColor" viewBox="0 0 20 20">
                <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM8.707 7.293a1 1 0 00-1.414 1.414L8.586 10l-1.293 1.293a1 1 0 101.414 1.414L10 11.414l1.293 1.293a1 1 0 001.414-1.414L11.414 10l1.293-1.293a1 1 0 00-1.414-1.414L10 8.586 8.707 7.293z" clip-rule="evenodd"></path>
              </svg>
            </div>
            <div class="ml-3">
              <p class="text-sm text-red-700 dark:text-red-300">{{ error }}</p>
            </div>
          </div>
        </div>

        <button
          type="submit"
          :disabled="loading"
          class="btn-primary w-full"
        >
          <span v-if="loading" class="flex items-center justify-center">
            <div class="w-4 h-4 border-2 border-white/30 border-t-white rounded-full animate-spin mr-2"></div>
            Sending...
          </span>
          <span v-else class="flex items-center justify-center">
            <svg class="w-4 h-4 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 19l9 2-9-18-9 18 9-2zm0 0v-8" />
            </svg>
            Send Message
          </span>
        </button>
      </form>
    </div>

    <!-- Messages List -->
    <div v-if="hasMessages" class="card p-6">
      <div class="mb-6">
        <h3 class="text-xl font-semibold text-gray-900 dark:text-white mb-2">Recent Messages</h3>
        <p class="text-dimmed">Messages from the community</p>
      </div>
      
      <div class="space-y-4">
        <div
          v-for="message in sortedMessages"
          :key="message.id"
          class="bg-gray-50/50 dark:bg-gray-800/50 backdrop-blur-sm rounded-lg p-4 border border-gray-200/50 dark:border-gray-700/50 hover:shadow-sm transition-all duration-200"
        >
          <div class="flex justify-between items-start">
            <div class="flex-1">
              <div class="flex items-center space-x-3 mb-2">
                <div class="w-8 h-8 bg-gradient-to-br from-primary-500 to-primary-600 rounded-full flex items-center justify-center">
                  <span class="text-xs font-medium text-white">{{ message.name.charAt(0).toUpperCase() }}</span>
                </div>
                <div>
                  <p class="text-sm font-medium text-gray-900 dark:text-white">{{ message.name }}</p>
                  <p class="text-xs text-dimmed">
                    {{ new Date(message.created_at).toLocaleString() }}
                  </p>
                </div>
              </div>
              <p class="text-sm text-gray-700 dark:text-gray-300 ml-11">{{ message.message }}</p>
            </div>
            <button
              @click="handleDelete(message.id)"
              class="ml-4 p-2 text-gray-400 hover:text-red-500 dark:text-gray-500 dark:hover:text-red-400 rounded-lg hover:bg-red-50 dark:hover:bg-red-500/10 transition-colors duration-200 group"
              title="Delete message"
            >
              <svg class="h-4 w-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16" />
              </svg>
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { reactive, onMounted } from 'vue'
import { storeToRefs } from 'pinia'
import { useHelloWorldStore } from '@/stores/helloWorld'

const store = useHelloWorldStore()
const { loading, error, hasMessages, sortedMessages } = storeToRefs(store)

const formData = reactive({
  name: '',
})

onMounted(async () => {
  await store.fetchMessages()
})

const handleSubmit = async () => {
  try {
    await store.createMessage(formData.name)
    formData.name = ''
  } catch (error) {
    console.error('Failed to create message:', error)
  }
}

const handleDelete = async (id) => {
  if (confirm('Are you sure you want to delete this message?')) {
    try {
      await store.deleteMessage(id)
    } catch (error) {
      console.error('Failed to delete message:', error)
    }
  }
}
</script> 