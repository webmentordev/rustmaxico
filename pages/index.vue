<template>
  <section class="bg-cover bg-center min-h-screen w-full relative" style="background-image: url('/header.webp')">
    <div class="bg-black/60 absolute top-0 left-0 w-full h-full backdrop-blur-sm">
      <div class="relative z-20 w-full h-full flex items-center justify-center">
        <div class="max-w-lg w-full bg-black/50 backdrop-blur-md border border-white/20 rounded-lg p-6 text-white">
          <div v-if="!pending" class="w-full">
            <!-- Section #0 -->
            <div class="text-center">
              <h1 class="text-5xl font-bold">Rust Mexico</h1>
              <div class="max-w-[380px] h-[1px] bg-white/20 m-auto my-3 rounded-full"></div>
              <p class="text-center w-full text-lg">US Comminuty - 1.5X Vanilla</p>
            </div>

            <div class="p-3 border border-white/10 mt-3">
              <div class="flex flex-col border-b border-white/10 pb-3">
                <div class="flex items-center justify-between">
                  <div class="flex items-center">
                    <h3 class="text-lg">Server Status</h3>
                    <img src="https://api.iconify.design/ant-design:thunderbolt-outlined.svg?color=%23f7d708"
                      width="18px">
                  </div>
                  <div class="flex items-center text-sm">
                    <h3>Last updated: </h3>
                    <span class="text-[#f7d708]">{{ time }}</span>
                    <button class="ml-1"><img
                        src="https://api.iconify.design/material-symbols:refresh-rounded.svg?color=%233af86a"
                        width="20px"></img></button>
                  </div>
                </div>
              </div>

              <div class="flex items-center justify-center py-4">
                <div v-if="status == 'online'"
                  class="py-2 px-4 mx-1 border border-green-500 text-green-500 flex items-center">
                  <img class="mr-2 animate-pulse"
                    src="https://api.iconify.design/majesticons:status-online-line.svg?color=%2345f514" width="20px">
                  <span>Online</span>
                </div>
                <div v-else class="py-2 px-4 mx-1 border border-red-500 text-red-500 flex items-center">
                  <img class="mr-2" src="https://api.iconify.design/radix-icons:cross-circled.svg?color=%23f53100"
                    width="20px">
                  <span>Offline</span>
                </div>
                <!-- <div class="py-2 px-4 mx-1 border border-[#fbff00] text-[#fbff00] flex items-center">
                  <img class="mr-2" src="https://api.iconify.design/codicon:pulse.svg?color=%23fbff00" width="20px">
                  <strong>{{ ping + 'ms' }}</strong>
                </div> -->
              </div>

              <div class="grid grid-cols-4">
                <div class="border border-white/10 p-2">
                  <div class="flex flex-col justify-center">
                    <div class="flex items-center mb-1">
                      <img src="https://api.iconify.design/material-symbols:person-3-outline.svg?color=%233af86a"
                        width="20px">
                      <strong class="text-sm mt-1">Players</strong>
                    </div>
                    <span class="m-auto w-fit">{{ players }}</span>
                  </div>
                </div>

                <div class="border border-white/10 p-2">
                  <div class="flex flex-col justify-center m-auto">
                    <div class="flex items-center mb-1 m-auto">
                      <img src="https://api.iconify.design/solar:ranking-broken.svg?color=%233af86a" width="20px">
                      <strong class="text-sm mt-1 ml-1">Rank</strong>
                    </div>
                    <span class="m-auto w-fit">#{{ rank }}</span>
                  </div>
                </div>

                <div class="border border-white/10 p-2">
                  <div class="flex flex-col justify-center m-auto">
                    <div class="flex items-center mb-1">
                      <img src="https://api.iconify.design/material-symbols:av-timer-rounded.svg?color=%233af86a"
                        width="20px">
                      <strong class="text-sm mt-1 ml-1">7 Days</strong>
                    </div>
                    <span class="m-auto w-fit">{{ firstdays }}</span>
                  </div>
                </div>

                <div class="border border-white/10 p-2">
                  <div class="flex flex-col justify-center m-auto">
                    <div class="flex items-center mb-1">
                      <img src="https://api.iconify.design/ic:outline-sentiment-satisfied.svg?color=%233af86a"
                        width="20px">
                      <strong class="text-sm mt-1 ml-1">30 Days</strong>
                    </div>
                    <span class="m-auto w-fit">{{ days }}</span>
                  </div>
                </div>
              </div>
              <div class="bg-[#3af86a] w-full h-[2px]"></div>
            </div>

            <!-- Section #02 -->
            <div class="p-3 border border-white/10 mt-3">
              <div class="flex flex-col border-b border-white/10 pb-3">
                <h3 class="text-2xl capitalize mb-2">Server Connection</h3>
                <div class="flex items-center justify-between">
                  <strong class="text-gray-400">{{ ip }}:{{ port }}</strong>
                  <a class="bg-[#fbff00] py-1 px-3 text-black font-bold"
                    :href='`steam://connect/${ip}:${port}`'>Connect</a>
                </div>
              </div>
            </div>

            <!-- Section #03 -->
            <div class="p-3 border border-white/10 mt-3">
              <div class="grid grid-cols-2 gap-2">
                <a href="https://discord.gg/HYnHFYyw" target="_blank" rel="nofollow"
                  class="flex items-center justify-center bg-[#7289da] p-2 rounded-lg">
                  <img src="https://api.iconify.design/flowbite:discord-solid.svg?color=%23ffffff" width="30">
                  <strong class="text-lg ml-2">Join Discord</strong>
                </a>
                <button class="flex items-center justify-center p-2 rounded-lg bg-white" @click="preview = true">
                  <img src="https://api.iconify.design/material-symbols:map-outline-rounded.svg?color=%23000000"
                    width="30">
                  <strong class="text-lg ml-2 text-black">Preview Map</strong>
                </button>
              </div>
              <div v-show="preview" class="fixed top-0 left-0 w-full h-full z-10">
                <div class="w-full h-full flex items-center justify-center bg-black/90 backdrop-blur-md relative">
                  <div class="max-w-[300px] w-full">
                    <img :src="mapUrl" class="w-full">
                  </div>
                  <button class="absolute bottom-2 right-2 bg-red-500 py-1 px-2" @click="preview = false">Close</button>
                </div>
              </div>
            </div>
          </div>
          <div class="flex items-center justify-center" v-else>
            <img src="https://api.iconify.design/svg-spinners:bars-scale.svg?color=%23ffffff" width="30px">
            <p class="ml-3">Fetching data please wait...</p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
const status = ref("online");
const preview = ref(false);
const time = ref("10:30 PM");
const ping = ref("...");
const players = ref("10/100");
const rank = ref("12,33");
const firstdays = ref("100%");
const days = ref("100%");
const ip = ref("192.168.100.1");
const port = ref("9987");
const serverID = '35520303';
const mapUrl = ref("https://content.rustmaps.com/maps/270/2f09b309d654494fb7f67490eca9696b/thumbnail.webp");
const pending = ref(false);

console.log(`${serverID}`);

await $fetch(`https://api.battlemetrics.com/servers/${serverID}`).then(result => {
  const now = new Date();
  const timeString = now.toLocaleTimeString([], {
    hour: '2-digit',
    minute: '2-digit',
    hour12: true
  });
  let record = result.data.attributes;
  status.value = record.status;
  time.value = timeString;
  players.value = record.players + "/" + record.maxPlayers;
  rank.value = record.rank;
  ip.value = record.ip;
  port.value = record.port;
  mapUrl.value = record.details.rust_maps.thumbnailUrl;
  pending.value = false;
});



</script>