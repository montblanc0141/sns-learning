<template>
  <!-- component -->
  <div class="flex flex-col">
    <div class="-my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
      <div class="py-2 align-middle inline-block min-w-full sm:px-6 lg:px-8">
        <div class="shadow overflow-hidden border-b border-gray-200">
          <table class="min-w-full">
            <thead class="bg-gray-50"></thead>
            <tbody class="bg-indigo-700">
              <tr>
                <td class="px-6 py-4 whitespace-nowrap">
                  <div class="flex items-center">
                    <div class="flex-shrink-0 h-16 w-16">
                      <img
                        class="h-16 w-16 rounded-full"
                        src="~assets/reshot-icon-video-marketing-9CFR4WBDEQ.svg"
                        alt=""
                      />
                    </div>
                    <div class="ml-4">
                      <div
                        class="text-2xl text-white font-light leading-normal"
                      >
                        Learn English from YouTube
                      </div>
                    </div>
                  </div>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive } from '@nuxtjs/composition-api'

export default defineComponent({
  setup() {
    const state = reactive({})
    return {
      state,
    }
  },
})
</script>

<style>
</style>