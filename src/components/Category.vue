<template>
    <div class="container mx-auto px-4 py-12 border-t border-gray-200">
      <h2 class="text-xl font-bold">{{ name }}</h2>
      <ul class="mt-4 grid grid-cols-1 gap-8 md:grid-cols-2 lg:grid-cols-3">
        <li
          v-for="test in tests"
          :key="test.name"
          class="relative py-6 flex flex-col rounded-lg border border-gray-200 overflow-hidden p-4 md:p-8"
          :class="{
            'border-gray-200': test.type === 'info' && typeof test.passed !== 'undefined',
            'border-gray-200': test.type !== 'success' && typeof test.passed === 'undefined',
            'border-gray-200': test.type === 'success' && typeof test.passed !== 'undefined',
            'border-yellow-600': test.type === 'warning' && typeof test.passed !== 'undefined',
            'border-red-600': test.type === 'error' && typeof test.passed !== 'undefined',
          }"
        >
          <div class="flex-1">
            <h3 class="font-semibold">{{ test.name }}</h3>
            <p class="mt-2 text-sm text-gray-700">{{ test.description }}</p>
          </div>
          <div v-if="test.comment" class="text-sm text-gray-700 p-4 rounded-lg border border-dashed mt-4 md:p-6">
            <h4 class="font-bold text-sm text-gray-800 mb-4">Comments</h4>
            {{ test.comment }}
          </div>
          <div class="absolute right-0 top-0">
            <div v-if="test.type === 'info'" class="inline-flex items-center justify-center uppercase text-xs font-medium text-blue-700 bg-blue-50 rounded py-1 px-2">
              <svg class="text-blue-600 w-6 h-6 mr-3" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"></path></svg>
              Info
            </div>
            <div v-else-if="test.type !== 'success' && typeof test.passed === 'undefined'" class="inline-flex items-center justify-center uppercase text-xs font-medium text-gray-700 bg-gray-50 rounded py-1 px-2">
              <svg class="text-gray-600 w-6 h-6 mr-3" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4m0 4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"></path></svg>
              Did not perform
            </div>
            <div v-else-if="test.type === 'error'" class="inline-flex items-center justify-center uppercase text-xs font-medium text-red-700 bg-red-50 rounded py-1 px-2">
              <svg class="text-red-600 w-6 h-6 mr-3" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4m0 4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"></path></svg>
              Error
            </div>
            <div v-else-if="test.type === 'success'" class="inline-flex items-center justify-center uppercase text-xs font-medium text-green-700 bg-green-50 rounded py-1 px-2">
              <svg class="text-green-600 w-6 h-6 mr-3" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z"></path></svg>
              Passed
            </div>
            <div v-else-if="test.type === 'warning'" class="inline-flex items-center justify-center uppercase text-xs font-medium text-yellow-700 bg-yellow-50 rounded py-1 px-2">
              <svg class="text-yellow-500 w-6 h-6 mr-3" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-3L13.732 4c-.77-1.333-2.694-1.333-3.464 0L3.34 16c-.77 1.333.192 3 1.732 3z"></path></svg>
              Warning
            </div>
          </div>
          <div class="text-right mt-4" v-if="test.infoUrl">
            <a :href="test.infoUrl" target="_blank" rel="noopener noreferrer" class="block text-center px-4 py-2 rounded border border-gray-400 text-gray-600 hover:bg-gray-600 hover:border-gray-600 hover:text-white transition duration-150">Learn more</a>
          </div>
        </li>
      </ul>
    </div>
</template>

<script>
export default {
  name: 'category',
  props: {
    name: {
      type: String,
      required: true
    },
    tests: {
      type: Array,
      required: true
    }
  }
}
</script>