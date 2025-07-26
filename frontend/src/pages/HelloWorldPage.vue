<template>
  <div class="px-4 sm:px-6 lg:px-8 py-8 w-full max-w-9xl mx-auto">
    
    <!-- Page Header -->
    <div class="mb-8">
      <div class="sm:flex sm:justify-between sm:items-center">
        <div class="mb-4 sm:mb-0">
          <div class="flex items-center space-x-3 mb-2">
            <div class="w-10 h-10 bg-gradient-to-br from-primary-500 to-primary-600 rounded-xl flex items-center justify-center">
              <svg class="w-5 h-5 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 12h.01M12 12h.01M16 12h.01M21 12c0 4.418-4.03 8-9 8a9.863 9.863 0 01-4.255-.949L3 20l1.395-3.72C3.512 15.042 3 13.574 3 12c0-4.418 4.03-8 9-8s9 3.582 9 8z" />
              </svg>
            </div>
            <div>
              <h1 class="text-2xl md:text-3xl font-bold text-gray-900 dark:text-white">Hello World API</h1>
              <p class="text-dimmed">Test the API integration with the Hello World service</p>
            </div>
          </div>
        </div>
        
        <!-- Breadcrumb -->
        <nav class="flex" aria-label="Breadcrumb">
          <ol class="flex items-center space-x-2">
            <li>
              <router-link to="/" class="text-dimmed hover:text-primary-600 dark:hover:text-primary-400 transition-colors">
                Home
              </router-link>
            </li>
            <li class="flex items-center">
              <svg class="w-4 h-4 text-gray-400 mx-2" fill="currentColor" viewBox="0 0 20 20">
                <path fill-rule="evenodd" d="M7.293 14.707a1 1 0 010-1.414L10.586 10 7.293 6.707a1 1 0 011.414-1.414l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414 0z" clip-rule="evenodd"></path>
              </svg>
              <span class="text-dimmed">Hello World</span>
            </li>
          </ol>
        </nav>
      </div>
    </div>

    <!-- Main Content -->
    <HelloWorldForm />

  </div>
</template>

<script setup>
import HelloWorldForm from '@/components/HelloWorld/HelloWorldForm.vue'
</script> 