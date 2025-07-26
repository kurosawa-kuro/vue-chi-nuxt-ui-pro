<template>
  <div class="px-4 sm:px-6 lg:px-8 py-8 w-full max-w-9xl mx-auto">
    <!-- Welcome Section -->
    <div class="mb-8">
      <div class="card bg-gradient-to-br from-primary-500 via-primary-600 to-primary-700 text-white p-8 shadow-xl border-0 overflow-hidden relative">
        <div class="absolute inset-0 bg-black/10"></div>
        <div class="absolute top-0 right-0 w-32 h-32 bg-white/10 rounded-full -translate-y-16 translate-x-16"></div>
        <div class="absolute bottom-0 left-0 w-24 h-24 bg-white/5 rounded-full translate-y-12 -translate-x-12"></div>
        <div class="relative text-center">
          <div class="w-16 h-16 bg-white/20 backdrop-blur-sm rounded-2xl flex items-center justify-center mx-auto mb-6">
            <svg class="w-8 h-8 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z" />
            </svg>
          </div>
          <h1 class="text-4xl font-bold mb-4">
            Welcome to Vue Chi Dashboard
          </h1>
          <p class="text-xl text-white/90 mb-8 max-w-2xl mx-auto leading-relaxed">
            A modern Vue 3 application with enterprise-grade components, beautiful design, and powerful backend integration
          </p>
          <div class="flex flex-col sm:flex-row gap-4 justify-center">
            <router-link
              to="/hello-world"
              class="inline-flex items-center px-8 py-4 bg-white dark:bg-gray-100 text-primary-600 dark:text-primary-700 font-semibold rounded-xl hover:bg-white/95 dark:hover:bg-gray-200 focus:outline-none focus:ring-2 focus:ring-white/20 dark:focus:ring-gray-300/20 transition-all duration-200 shadow-lg"
            >
              <svg class="w-5 h-5 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 12h.01M12 12h.01M16 12h.01M21 12c0 4.418-4.03 8-9 8a9.863 9.863 0 01-4.255-.949L3 20l1.395-3.72C3.512 15.042 3 13.574 3 12c0-4.418 4.03-8 9-8s9 3.582 9 8z" />
              </svg>
              Try Hello World API
            </router-link>
            <button class="inline-flex items-center px-8 py-4 bg-white/10 backdrop-blur-sm text-white font-semibold rounded-xl hover:bg-white/20 focus:outline-none focus:ring-2 focus:ring-white/20 transition-all duration-200 border border-white/20">
              <svg class="w-5 h-5 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
              </svg>
              View Documentation
            </button>
          </div>
        </div>
      </div>
    </div>

    <!-- Features Grid -->
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6 mb-8">
      <!-- Feature Card 1 -->
      <div class="card p-6">
        <div class="flex items-center justify-center w-12 h-12 bg-violet-100 dark:bg-violet-900/20 rounded-lg mb-4">
          <svg class="w-6 h-6 text-violet-600 dark:text-violet-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z" />
          </svg>
        </div>
        <h3 class="text-lg font-semibold text-gray-900 dark:text-gray-100 mb-2">Lightning Fast</h3>
        <p class="text-dimmed text-sm leading-relaxed">
          Built with Vite for instant hot module replacement and optimized build performance.
        </p>
      </div>

      <!-- Feature Card 2 -->
      <div class="card p-6">
        <div class="flex items-center justify-center w-12 h-12 bg-emerald-100 dark:bg-emerald-900/20 rounded-lg mb-4">
          <svg class="w-6 h-6 text-emerald-600 dark:text-emerald-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 7v10c0 2.21 3.582 4 8 4s8-1.79 8-4V7M4 7c0 2.21 3.582 4 8 4s8-1.79 8-4M4 7c0-2.21 3.582-4 8-4s8 1.79 8 4" />
          </svg>
        </div>
        <h3 class="text-lg font-semibold text-gray-900 dark:text-gray-100 mb-2">State Management</h3>
        <p class="text-dimmed text-sm leading-relaxed">
          Powered by Pinia for intuitive and type-safe state management across your application.
        </p>
      </div>

      <!-- Feature Card 3 -->
      <div class="card p-6">
        <div class="flex items-center justify-center w-12 h-12 bg-blue-100 dark:bg-blue-900/20 rounded-lg mb-4">
          <svg class="w-6 h-6 text-blue-600 dark:text-blue-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M7 21a4 4 0 01-4-4V5a2 2 0 012-2h4a2 2 0 012 2v12a4 4 0 01-4 4zM21 5a2 2 0 00-2-2h-4a2 2 0 00-2 2v12a4 4 0 004 4h4a2 2 0 002-2V5z" />
          </svg>
        </div>
        <h3 class="text-lg font-semibold text-gray-900 dark:text-gray-100 mb-2">Modern Design</h3>
        <p class="text-dimmed text-sm leading-relaxed">
          Crafted with Tailwind CSS and professional UI components for beautiful interfaces.
        </p>
      </div>

      <!-- Feature Card 4 -->
      <div class="card p-6">
        <div class="flex items-center justify-center w-12 h-12 bg-amber-100 dark:bg-amber-900/20 rounded-lg mb-4">
          <svg class="w-6 h-6 text-amber-600 dark:text-amber-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20.354 15.354A9 9 0 018.646 3.646 9.003 9.003 0 0012 21a9.003 9.003 0 008.354-5.646z" />
          </svg>
        </div>
        <h3 class="text-lg font-semibold text-gray-900 dark:text-gray-100 mb-2">Dark Mode</h3>
        <p class="text-dimmed text-sm leading-relaxed">
          Complete dark mode support with smooth transitions and consistent theming.
        </p>
      </div>

      <!-- Feature Card 5 -->
      <div class="card p-6">
        <div class="flex items-center justify-center w-12 h-12 bg-rose-100 dark:bg-rose-900/20 rounded-lg mb-4">
          <svg class="w-6 h-6 text-rose-600 dark:text-rose-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 18h.01M8 21h8a2 2 0 002-2V5a2 2 0 00-2-2H8a2 2 0 00-2 2v14a2 2 0 002 2z" />
          </svg>
        </div>
        <h3 class="text-lg font-semibold text-gray-900 dark:text-gray-100 mb-2">Responsive</h3>
        <p class="text-dimmed text-sm leading-relaxed">
          Fully responsive design that works perfectly on desktop, tablet, and mobile devices.
        </p>
      </div>

      <!-- Feature Card 6 -->
      <div class="card p-6">
        <div class="flex items-center justify-center w-12 h-12 bg-indigo-100 dark:bg-indigo-900/20 rounded-lg mb-4">
          <svg class="w-6 h-6 text-indigo-600 dark:text-indigo-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" />
          </svg>
        </div>
        <h3 class="text-lg font-semibold text-gray-900 dark:text-gray-100 mb-2">Type Safe</h3>
        <p class="text-dimmed text-sm leading-relaxed">
          Built with TypeScript support and comprehensive testing for reliable applications.
        </p>
      </div>
    </div>

    <!-- Placeholder Images Section -->
    <PlaceholderImages />

    <!-- Stats Section -->
    <div class="card p-8">
      <div class="text-center mb-8">
        <h2 class="text-2xl font-bold text-gray-900 dark:text-white mb-2">Built for Performance</h2>
        <p class="text-dimmed">Powerful features and enterprise-grade capabilities</p>
      </div>
      <div class="grid grid-cols-1 md:grid-cols-4 gap-8">
        <div class="text-center group">
          <div class="w-16 h-16 bg-gradient-to-br from-primary-500 to-primary-600 rounded-2xl flex items-center justify-center mx-auto mb-4 group-hover:scale-110 transition-transform duration-200">
            <svg class="w-8 h-8 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 11H5m14 0a2 2 0 012 2v6a2 2 0 01-2 2H5a2 2 0 01-2-2v-6a2 2 0 012-2m14 0V9a2 2 0 00-2-2M5 11V9a2 2 0 012-2m0 0V5a2 2 0 012-2h6a2 2 0 012 2v2M7 7h10" />
            </svg>
          </div>
          <div class="text-3xl font-bold text-primary-600 dark:text-primary-400 mb-2">100+</div>
          <div class="text-sm font-medium text-dimmed">Components</div>
        </div>
        <div class="text-center group">
          <div class="w-16 h-16 bg-gradient-to-br from-emerald-500 to-emerald-600 rounded-2xl flex items-center justify-center mx-auto mb-4 group-hover:scale-110 transition-transform duration-200">
            <svg class="w-8 h-8 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z" />
            </svg>
          </div>
          <div class="text-3xl font-bold text-emerald-600 dark:text-emerald-400 mb-2">50+</div>
          <div class="text-sm font-medium text-dimmed">Page Templates</div>
        </div>
        <div class="text-center group">
          <div class="w-16 h-16 bg-gradient-to-br from-blue-500 to-blue-600 rounded-2xl flex items-center justify-center mx-auto mb-4 group-hover:scale-110 transition-transform duration-200">
            <svg class="w-8 h-8 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20 7l-8-4-8 4m16 0l-8 4m8-4v10l-8 4m0-10L4 7m8 4v10M4 7v10l8 4" />
            </svg>
          </div>
          <div class="text-3xl font-bold text-blue-600 dark:text-blue-400 mb-2">15+</div>
          <div class="text-sm font-medium text-dimmed">Demo Apps</div>
        </div>
        <div class="text-center group">
          <div class="w-16 h-16 bg-gradient-to-br from-rose-500 to-rose-600 rounded-2xl flex items-center justify-center mx-auto mb-4 group-hover:scale-110 transition-transform duration-200">
            <svg class="w-8 h-8 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M18.364 5.636l-3.536 3.536m0 5.656l3.536 3.536M9.172 9.172L5.636 5.636m3.536 9.192L5.636 18.364M21 12a9 9 0 11-18 0 9 9 0 0118 0zm-5 0a4 4 0 11-8 0 4 4 0 018 0z" />
            </svg>
          </div>
          <div class="text-3xl font-bold text-rose-600 dark:text-rose-400 mb-2">24/7</div>
          <div class="text-sm font-medium text-dimmed">Support</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import PlaceholderImages from '@/components/PlaceholderImages.vue'
</script> 