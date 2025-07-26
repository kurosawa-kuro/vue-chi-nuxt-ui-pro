<template>
  <div class="p-6 space-y-6">
    <h2 class="text-2xl font-bold text-gray-900 dark:text-white">
      Placeholder Images
    </h2>
    
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
      <!-- Vue + Chi Logo -->
      <div class="bg-white dark:bg-gray-800 p-4 rounded-lg shadow">
        <h3 class="text-lg font-semibold mb-3 text-gray-900 dark:text-white">Vue + Chi</h3>
        <img 
          src="https://via.placeholder.com/32/00DC82/ffffff?text=VC" 
          alt="Vue Chi Logo"
          class="w-32 h-32 mx-auto"
        />
        <p class="text-sm text-gray-600 dark:text-gray-400 mt-2 text-center">
          32x32 Green Badge
        </p>
      </div>

      <!-- John Doe Avatar -->
      <div class="bg-white dark:bg-gray-800 p-4 rounded-lg shadow">
        <h3 class="text-lg font-semibold mb-3 text-gray-900 dark:text-white">User Avatar</h3>
        <img 
          src="https://via.placeholder.com/32/6B7280/ffffff?text=JD" 
          alt="John Doe Avatar"
          class="w-32 h-32 mx-auto rounded-full"
        />
        <p class="text-sm text-gray-600 dark:text-gray-400 mt-2 text-center">
          32x32 Gray Avatar
        </p>
      </div>

      <!-- Larger Variants -->
      <div class="bg-white dark:bg-gray-800 p-4 rounded-lg shadow">
        <h3 class="text-lg font-semibold mb-3 text-gray-900 dark:text-white">Larger Variants</h3>
        <div class="flex items-center justify-center space-x-4">
          <img 
            src="https://via.placeholder.com/64/00DC82/ffffff?text=VC" 
            alt="Vue Chi Logo 64x64"
            class="w-16 h-16"
          />
          <img 
            src="https://via.placeholder.com/64/6B7280/ffffff?text=JD" 
            alt="John Doe Avatar 64x64"
            class="w-16 h-16 rounded-full"
          />
        </div>
        <p class="text-sm text-gray-600 dark:text-gray-400 mt-2 text-center">
          64x64 Versions
        </p>
      </div>

      <!-- Different Colors -->
      <div class="bg-white dark:bg-gray-800 p-4 rounded-lg shadow">
        <h3 class="text-lg font-semibold mb-3 text-gray-900 dark:text-white">Color Variants</h3>
        <div class="grid grid-cols-3 gap-2">
          <img 
            src="https://via.placeholder.com/40/3B82F6/ffffff?text=B" 
            alt="Blue"
            class="w-10 h-10 mx-auto"
          />
          <img 
            src="https://via.placeholder.com/40/EF4444/ffffff?text=R" 
            alt="Red"
            class="w-10 h-10 mx-auto"
          />
          <img 
            src="https://via.placeholder.com/40/10B981/ffffff?text=G" 
            alt="Green"
            class="w-10 h-10 mx-auto"
          />
          <img 
            src="https://via.placeholder.com/40/F59E0B/ffffff?text=Y" 
            alt="Yellow"
            class="w-10 h-10 mx-auto"
          />
          <img 
            src="https://via.placeholder.com/40/8B5CF6/ffffff?text=P" 
            alt="Purple"
            class="w-10 h-10 mx-auto"
          />
          <img 
            src="https://via.placeholder.com/40/EC4899/ffffff?text=PK" 
            alt="Pink"
            class="w-10 h-10 mx-auto"
          />
        </div>
        <p class="text-sm text-gray-600 dark:text-gray-400 mt-2 text-center">
          40x40 Color Collection
        </p>
      </div>

      <!-- Banner Size -->
      <div class="bg-white dark:bg-gray-800 p-4 rounded-lg shadow md:col-span-2">
        <h3 class="text-lg font-semibold mb-3 text-gray-900 dark:text-white">Banner Example</h3>
        <img 
          src="https://via.placeholder.com/400x200/00DC82/ffffff?text=Vue+Chi+Banner" 
          alt="Vue Chi Banner"
          class="w-full max-w-md mx-auto"
        />
        <p class="text-sm text-gray-600 dark:text-gray-400 mt-2 text-center">
          400x200 Banner
        </p>
      </div>
    </div>

    <!-- URL Examples -->
    <div class="bg-gray-50 dark:bg-gray-900 p-4 rounded-lg">
      <h3 class="text-lg font-semibold mb-3 text-gray-900 dark:text-white">
        URL Examples
      </h3>
      <div class="space-y-2 text-sm font-mono">
        <div class="text-gray-600 dark:text-gray-400">
          https://via.placeholder.com/32/00DC82/ffffff?text=VC
        </div>
        <div class="text-gray-600 dark:text-gray-400">
          https://via.placeholder.com/32/6B7280/ffffff?text=JD
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
// No JavaScript needed for this static component
</script>