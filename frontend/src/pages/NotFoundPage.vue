<template>
  <div class="min-h-screen bg-gray-50 dark:bg-gray-900 flex items-center justify-center px-4 sm:px-6 lg:px-8">
    <div class="max-w-lg w-full">
      <div class="card p-8 text-center">
        <!-- Error Illustration -->
        <div class="mb-8">
          <div class="relative mx-auto w-32 h-32">
            <div class="absolute inset-0 bg-gradient-to-br from-primary-500/20 to-primary-600/20 rounded-full animate-pulse"></div>
            <div class="absolute inset-4 bg-gradient-to-br from-primary-500 to-primary-600 rounded-full flex items-center justify-center">
              <svg class="w-12 h-12 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9.172 16.172a4 4 0 015.656 0M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
              </svg>
            </div>
          </div>
        </div>

        <!-- Error Content -->
        <div class="mb-8">
          <div class="mb-4">
            <span class="inline-flex items-center px-4 py-2 bg-primary-50 dark:bg-primary-500/10 text-primary-700 dark:text-primary-400 rounded-full text-sm font-medium">
              Error 404
            </span>
          </div>
          <h1 class="text-4xl font-bold text-gray-900 dark:text-white mb-4">
            Page Not Found
          </h1>
          <p class="text-lg text-dimmed leading-relaxed max-w-md mx-auto">
            Sorry, we couldn't find the page you're looking for. The page may have been moved, deleted, or you may have entered an incorrect URL.
          </p>
        </div>

        <!-- Action Buttons -->
        <div class="space-y-4">
          <router-link
            to="/"
            class="btn-primary w-full"
          >
            <svg class="w-5 h-5 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6"></path>
            </svg>
            Return to Homepage
          </router-link>
          
          <button
            @click="$router.go(-1)"
            class="btn-secondary w-full"
          >
            <svg class="w-5 h-5 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 19l-7-7m0 0l7-7m-7 7h18"></path>
            </svg>
            Go Back
          </button>
        </div>

        <!-- Help Links -->
        <div class="mt-8 pt-6 border-t border-gray-200 dark:border-gray-700">
          <p class="text-sm text-dimmed mb-4">Need help? Try these popular pages:</p>
          <div class="flex flex-wrap justify-center gap-4">
            <router-link to="/" class="text-sm text-primary-600 dark:text-primary-400 hover:text-primary-700 dark:hover:text-primary-300 transition-colors">
              Home
            </router-link>
            <router-link to="/hello-world" class="text-sm text-primary-600 dark:text-primary-400 hover:text-primary-700 dark:hover:text-primary-300 transition-colors">
              Hello World
            </router-link>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
// コンポーネントロジック
</script> 