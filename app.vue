<template>
  <div class="mt-5 md:col-span-2 md:mt-0">
    <div class="space-y-6 bg-white px-4 py-5 sm:p-6">

      <div class="grid grid-cols-3 gap-6">
        <div class="col-span-3 sm:col-span-2">
          <label for="playerUrl" class="block text-sm font-medium text-gray-700">Signed Player Url</label>
          <div class="mt-1 flex rounded-md shadow-sm">
            <input type="text" name="playerUrl" v-model="playerUrl"
                   class="block w-full flex-1
                   rounded-none
                   rounded-r-md
                   border-gray-700
                   focus:border-indigo-500
                   focus:ring-indigo-500
                   sm:text-sm"/>
          </div>
        </div>
      </div>

      <div class="grid grid-cols-3 gap-6">
        <div class="col-span-3 sm:col-span-2">
          <label for="setting" class="block text-sm font-medium text-gray-700">JWPlayer setting</label>
          <div class="mt-1 flex rounded-md shadow-sm">
            <textarea name="setting" v-model="setting"
                      placeholder='{ "playlist": [{}] }'
                      class="mt-1 block w-full
                      rounded-md
                      border-gray-700
                      shadow-sm
                      focus:border-indigo-500
                      focus:ring-indigo-500
                      sm:text-sm h-64"/>
          </div>
        </div>
      </div>

      <div class="bg-gray-50 px-4 py-3 sm:px-6">
        <button @click="play"
                class="inline-flex justify-center
                rounded-md border border-transparent
                bg-indigo-600 py-2 px-4
                text-sm font-medium
                text-white shadow-sm hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2">
          Play
        </button>
      </div>

      <div class="px-6 py-4 pb-2">
        <div id="player"></div>
      </div>
    </div>
  </div>
</template>

<script>
import {loadScript} from "vue-plugin-load-script";

export default {
  data() {

    return {
      playerUrl: '',
      setting: `{
    "playlist": [
        {
            "adschedule": "",
            "file": "",
            "mediaid": ""
        }
    ]
}`,
    }
  },
  methods: {
    play() {
      loadScript(this.playerUrl).then(() => {
        try {
          const jwSetting = JSON.parse(this.setting)
          console.log(jwSetting);
          window['jwplayer']("player").setup(jwSetting);
        } catch (e) {
          console.error(e)
        }
      })
    }
  }
}
</script>
