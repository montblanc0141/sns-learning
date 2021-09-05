<template>
  <div>
    <div
      class="
        flex
        items-center
        py-6
        pl-6
        space-x-4
        bg-white
        rounded-xl
        overflow-x-auto
        shadow-lg
        hover:shadow-xl hover:scale-105
        transition
        duration-500
      "
    >
      <div class="flex bg-gray-100 p-4 w-72 space-x-4 rounded-lg">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-6 w-6 opacity-30"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"
          />
        </svg>
        <input
          class="bg-gray-100 outline-none"
          type="text"
          placeholder="Add keyword"
          v-model="keyword"
        />
      </div>
      <div>Get</div>
      <div class="relative inline-flex">
        <svg
          class="w-2 h-2 absolute top-0 right-0 m-4 pointer-events-none"
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 412 232"
        >
          <path
            d="M206 171.144L42.678 7.822c-9.763-9.763-25.592-9.763-35.355 0-9.763 9.764-9.763 25.592 0 35.355l181 181c4.88 4.882 11.279 7.323 17.677 7.323s12.796-2.441 17.678-7.322l181-181c9.763-9.764 9.763-25.592 0-35.355-9.763-9.763-25.592-9.763-35.355 0L206 171.144z"
            fill="#648299"
            fill-rule="nonzero"
          />
        </svg>
        <select
          v-model="selected"
          class="
            border border-gray-300
            rounded-full
            text-gray-600
            h-10
            pl-5
            pr-10
            w-20
            bg-white
            hover:border-gray-400
            focus:outline-none
            appearance-none
          "
        >
          <option
            v-for="option in options"
            :key="option.text"
            :value="option.value"
          >
            {{ option.text }}
          </option>
        </select>
      </div>
      <div>Videos</div>
      <div class="flex justify-center items-center">
        <div
          class="
            relative
            rounded-full
            w-12
            h-6
            transition
            duration-200
            ease-linear
          "
          :class="toggle === '1' ? 'bg-green-400' : 'bg-gray-400'"
        >
          <label
            for="toggle"
            class="
              absolute
              left-0
              bg-white
              border-2
              mb-2
              w-6
              h-6
              rounded-full
              transition
              transform
              duration-100
              ease-linear
              cursor-pointer
            "
            :class="[
              toggle === '1'
                ? 'translate-x-full border-green-400'
                : 'translate-x-0 border-gray-400',
            ]"
          ></label>
          <input
            type="checkbox"
            id="toggle"
            name="toggle"
            class="
              appearance-none
              w-full
              h-full
              active:outline-none
              focus:outline-none
            "
            @click="toggle === '0' ? (toggle = '1') : (toggle = '0')"
          />
        </div>
      </div>
      <div>Uploaded Recently</div>
      <div
        class="
          bg-red-600
          py-3
          px-5
          text-white
          font-semibold
          rounded-lg
          hover:shadow-lg
          transition
          duration-3000
          cursor-pointer
        "
      >
        <span @click="getVideos">Search</span>
      </div>
    </div>
    <div class="flex flex-col">
      <div class="-my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
        <div class="py-2 align-middle inline-block min-w-full sm:px-6 lg:px-8">
          <div
            class="
              shadow
              overflow-hidden
              border-b border-gray-200
              sm:rounded-lg
            "
          >
            <table class="min-w-full divide-y divide-gray-200">
              <thead class="bg-gray-50">
                <tr>
                  <th
                    scope="col"
                    class="
                      px-8
                      py-3
                      text-left text-xs
                      font-medium
                      text-gray-500
                      uppercase
                      tracking-wider
                    "
                  >
                    #
                  </th>
                  <th
                    scope="col"
                    class="
                      px-6
                      py-3
                      text-left text-xs
                      font-medium
                      text-gray-500
                      uppercase
                      tracking-wider
                    "
                  >
                    Video
                  </th>
                  <th
                    scope="col"
                    class="
                      px-6
                      py-3
                      text-left text-xs
                      font-medium
                      text-gray-500
                      uppercase
                      tracking-wider
                    "
                  >
                    Title
                  </th>
                  <th
                    scope="col"
                    class="
                      px-6
                      py-3
                      text-left text-xs
                      font-medium
                      text-gray-500
                      uppercase
                      tracking-wider
                    "
                  >
                    Upload Date
                  </th>
                  <th
                    scope="col"
                    class="
                      px-6
                      py-3
                      text-left text-xs
                      font-medium
                      text-gray-500
                      uppercase
                      tracking-wider
                    "
                  >
                    Description
                  </th>
                </tr>
              </thead>
              <tbody class="bg-white divide-y divide-gray-200">
                <tr v-for="(result, index) in results" :key="result.id.videoId">
                  <td class="px-6 py-4">
                    <span
                      class="
                        inline-flex
                        px-3
                        py-2
                        font-semibold
                        leading-5
                        rounded-full
                        bg-green-100
                        text-green-800
                      "
                      >{{ index + 1 }}</span
                    >
                  </td>
                  <td class="px-6 py-4">
                    <div class="flex items-center">
                      <div>
                        <a
                          :href="
                            'https://www.youtube.com/watch?v=' +
                            result.id.videoId
                          "
                        >
                          <img
                            width="600"
                            height="400"
                            :src="result.snippet.thumbnails.medium.url"
                          />
                        </a>
                      </div>
                    </div>
                  </td>
                  <td class="px-6 py-4">
                    <div class="text-sm text-gray-900">
                      {{ result.snippet.title }}
                    </div>
                    <div class="text-sm text-gray-500">
                      {{ result.snippet.channelTitle }}
                    </div>
                  </td>
                  <td class="px-6 py-4 whitespace-nowrap">
                    <span
                      class="
                        text-left text-xs
                        font-medium
                        text-gray-500
                        uppercase
                        tracking-wider
                      "
                    >
                      {{ result.snippet.publishedAt.substr(0, 10) }}
                    </span>
                  </td>
                  <td class="px-6 py-4 text-sm text-gray-500">
                    {{ result.snippet.description }}
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
    <div
      class="flex items-center justify-center w-full h-full pt-2"
      v-if="loadning"
    >
      <div
        class="flex justify-center items-center space-x-1 text-sm text-gray-700"
      >
        <svg
          fill="none"
          class="w-6 h-6 animate-spin"
          viewBox="0 0 32 32"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            clip-rule="evenodd"
            d="M15.165 8.53a.5.5 0 01-.404.58A7 7 0 1023 16a.5.5 0 011 0 8 8 0 11-9.416-7.874.5.5 0 01.58.404z"
            fill="currentColor"
            fill-rule="evenodd"
          />
        </svg>

        <div>Loading ...</div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, watch } from '@nuxtjs/composition-api'
import axios from 'axios'
import moment from 'moment'

export default defineComponent({
  setup() {
    let toggle = ref<String>('0')
    let selected = ref<any>('5')
    let options = [
      { text: '5', value: '5' },
      { text: '10', value: '10' },
      { text: '25', value: '25' },
      { text: '50', value: '50' },
    ]
    let results = ref<any[]>()

    let loading = ref<Boolean>(false)

    let keyword = ref<String>()

    const params = {
      q: keyword.value,
      part: 'snippet',
      type: 'video',
      maxResults: '5',
      order: 'relevance',
      regionCode: 'JP',
      videoCategoryId: '27',
      publishedAfter: '',
      key: process.env.API_KEY,
    }

    watch([keyword, selected, selected], () => updateParams())

    function updateParams() {
      console.log(selected.value)
      params.q = keyword.value
      if (selected.value != '5') {
        params.maxResults = selected.value
      }
    }

    function getVideos() {
      loading.value = true
      if (toggle.value == '1') {
        params.publishedAfter = moment(Date.now()).add(-1, 'months').format()
      } else {
        params.publishedAfter = moment(Date.now()).add(-10, 'years').format()
      }
      console.log(params)
      axios
        .get('https://www.googleapis.com/youtube/v3/search', {
          params: params,
        })
        .then(function (res) {
          results.value = res.data.items
          console.log(results.value)
          loading.value = false
        })
    }

    return {
      getVideos,
      results,
      keyword,
      loading,
      toggle,
      selected,
      options,
    }
  },
})
</script>

<style>
</style>