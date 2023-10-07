<template>
  <div class="bg-dark h-screen">
    <div class="flex h-[88vh]">
      <!--Side Nav-->
      <div class="w-56 flex-none bg-black h-full">
        <div class="p-6 cursor-pointer">
          <img src="spotifyLogo.png" alt="" class="h-9" />
        </div>
        <div class="mx-2 mb-7">
          <button v-for="tab in tabs" @click="id = tab.id" :class="`w-full rounded px-3 py-2 flex items-center justify-start text-sm hover:text-white font-semibold ${id == tab.id ? 'bg-light text-white' : 'text-lightest'
            }`">
            <i :class="`mr-3 text-xl  ${tab.icon}`"></i>
            <p class="">{{ tab.name }}</p>
          </button>
        </div>
        <div class="mx-5">
          <button
            class="flex items-center justify-start text-white text-xs font-semibold opacity-75 hover:opacity-100 transition-all duration-300 mb-3">
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5"
              stroke="currentColor" class="w-6 h-6 mr-3 bg-white text-black">
              <path stroke-linecap="round" stroke-linejoin="round" d="M12 4.5v15m7.5-7.5h-15" />
            </svg>Create playlist
          </button>
          <button
            class="flex items-center justify-start text-white text-xs font-semibold opacity-75 hover:opacity-100 transition-all duration-300">
            <img src="liked_song.jpeg" alt="" class="w-6 h-6 mr-3" />Liked songs
          </button>
          <div class="w-full h-[1px] my-3 bg-light"></div>
        </div>
        <div class="mx-5">
          <div
            class="w-full overflow-y-scroll h-48 scrollbar-thin scrollbar-track-inherit shadow-md scrollbar-thumb-lightest">
            <p v-for="playlist in playlists" class="text-lightest hover:text-white text-xs font-medium py-2">
              {{ playlist.name.substring(0, 20) + "..." }}
            </p>
          </div>
          <button class="flex items-center justify-start text-lightest hover:text-white py-2">
            <i class="fa-regular fa-circle-down mr-4 text-xl"></i>
            <p class="text-sm font-semi-bold">Install app</p>
          </button>
        </div>
      </div>
      <!--Main Content-->
      <div
        class="w-full h-full relative overflow-y-scroll scrollbar-thin scrollbar-track-inherit scrollbar-thumb-lightest">
        <!--Header-->
        <div
          class="w-full top-0 sticky py-4 px-6 flex items-center justify-between backdrop-filter backdrop-blur-lg bg-opacity-30 z-10">
          <div class="flex items-center">
            <button class="rounded-full w-8 h-8 bg-black cursor-not-allowed text-lightest mr-3">
              <i class="fa-solid fa-chevron-left text-xl"></i>
            </button>
            <button class="rounded-full w-8 h-8 bg-black cursor-not-allowed text-lightest">
              <i class="fa-solid fa-chevron-right text-xl"></i>
            </button>
          </div>
          <div class="relative">
            <button @click="dropdown = !dropdown"
              class="bg-light rounded-full py-1 px-2 flex items-center transition-all duration-300">
              <img src="matty_healy.jpg" alt="" class="w-7 h-7 rounded-full mr-2 object-cover" />
              <p class="text-xs font-bold text-white mr-2">Matty Healy</p>
              <i :class="`bx bxs-down-arrow text-white text-xs ${dropdown ? 'rotate-180' : ''
                }`"></i>
            </button>
            <div v-if="dropdown" class="absolute w-48 bg-light p-1 rounded-sm mt-1 right-1/2">
              <button v-for="dropdown in profile_dropdowns"
                class="w-full py-2 text-lightest p-4 mb-3 hover:text-white hover:bg-lightest transition-all duration-300 flex items-center justify-between font-bold">
                <p class="text-xs">{{ dropdown.name }}</p>
                <i :class="`${dropdown.icon} text-xs`"></i>
              </button>
              <div class="w-full h-[1px] my-1 bg-lightest"></div>
              <button class="w-full py-2 text-lightest p-4 hover:text-white hover:bg-lightest font-bold flex">
                <p class="text-xs">Log out</p>
              </button>
            </div>
          </div>
        </div>
        <!--Cards-->
        <div class="py-4 px-7">
          <div class="flex items-center justify-between w-full mb-3">
            <h1 class="text-xl text-white font-bold tracking-wider hover:underline cursor-pointer">
              Recently played
            </h1>
            <h2 class="text-xs hover:underline font-semibold cursor-pointer text-lightest tracking-wider">
              Show all
            </h2>
          </div>
          <div class="w-full flex flex-wrap">
            <div class="w-[13.2rem] p-3 cursor-pointer" v-for="recent in recents">
              <div class="bg-light relative rounded-lg w-full h-full p-5">
                <div
                  class="absolute w-full h-full flex items-center justify-end p-8 opacity-0 transition-all duration-500 hover:opacity-100">
                  <div class="bg-green rounded-full h-12 w-12 flex items-center justify-center">
                    <i class="fa-solid fa-play text-xl"></i>
                  </div>
                </div>
                <img :src="`${recent.img}`" alt="" class="h-auto w-full shadow rounded-md mb-3" />
                <h3 class="text-sm font-semibold text-white tracking-wider mb-3">
                  {{ recent.title }}
                </h3>
                <h4 class="text-xs font-semibold text-lightest tracking-wider pb-3">
                  {{ recent.artist }}
                </h4>
              </div>
            </div>
          </div>
        </div>
        <div class="py-4 px-7">
          <div class="flex items-center justify-between w-full mb-3">
            <h1 class="text-xl text-white font-bold tracking-wider hover:underline cursor-pointer">
              Made for Matty
            </h1>
            <h2 class="text-xs hover:underline font-semibold cursor-pointer text-lightest tracking-wider">
              Show all
            </h2>
          </div>
          <div class="w-full flex flex-wrap pb-3">
            <div class="w-[13.2rem] p-3 cursor-pointer" v-for="matt in matty">
              <div class="bg-light relative rounded-lg w-full h-full p-5">
                <div
                  class="absolute w-full h-full flex items-center justify-end p-8 opacity-0 transition-all duration-500 hover:opacity-100">
                  <div class="bg-green rounded-full h-12 w-12 flex items-center justify-center">
                    <i class="fa-solid fa-play text-xl"></i>
                  </div>
                </div>
                <img :src="`${matt.img}`" alt="" class="h-auto w-full shadow rounded-md mb-3" />
                <h3 class="text-sm font-semibold text-white tracking-wider mb-3">
                  {{ matt.title }}
                </h3>
                <h4 class="text-xs font-semibold text-lightest tracking-wider pb-3">
                  {{ matt.artist }}
                </h4>
              </div>
            </div>
          </div>
        </div>
        <div class="py-4 px-7">
          <div class="flex items-center justify-between w-full mb-3">
            <h1 class="text-xl text-white font-bold tracking-wider hover:underline cursor-pointer">
              Recently played
            </h1>
            <h2 class="text-xs hover:underline font-semibold cursor-pointer text-lightest tracking-wider">
              Show all
            </h2>
          </div>
          <div class="w-full flex flex-wrap">
            <div class="w-[13.2rem] p-3 cursor-pointer" v-for="best in bests">
              <div class="bg-light rounded-lg w-full h-full p-5 relative">
                <div
                  class="absolute w-full h-full flex items-center justify-end p-8 opacity-0 transition-all duration-500 hover:opacity-100">
                  <div class="bg-green rounded-full h-12 w-12 flex items-center justify-center">
                    <i class="fa-solid fa-play text-xl"></i>
                  </div>
                </div>
                <img :src="`${best.img}`" alt="" class="h-auto w-full shadow rounded-md mb-3" />
                <h3 class="text-sm font-semibold text-white tracking-wider mb-3">
                  {{ best.title }}
                </h3>
                <h4 class="text-xs font-semibold text-lightest tracking-wider pb-1 leading-loose">
                  {{ best.artist }}
                </h4>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!--Play Bar-->
    <div class="w-full bg-light h-[13vh] flex items-center justify-between px-3">
      <div class="flex items-center cursor-pointer">
        <img src="BFIAGL.jpeg" alt="" class="w-14 h-14" />
        <div class="ml-2">
          <h1 class="text-sm text-white">Human Too</h1>
          <h2 class="text-xs text-lightest font-semibold">The 1975</h2>
        </div>
        <div class="ml-4">
          <i class="fa-solid fa-heart text-base text-green"></i>
        </div>
      </div>
      <div class="flex flex-col justify-center -mt-3 w-1/3 items-center cursor-pointer">
        <div class="flex items-center gap-10">
          <button class="text-lg text-lightest hover:text-white">
            <i class="fa-solid fa-shuffle"></i>
          </button>
          <button class="text-lg text-lightest hover:text-white">
            <i class="fa-solid fa-backward-step"></i>
          </button>
          <button class=" text-dark">
            <i
              class="fa-solid fa-play border text-lg border-lightest rounded-full bg-white h-10 w-10 flex items-center justify-center"></i>
          </button>

          <button class="text-lg text-lightest hover:text-white">
            <i class="fa-solid fa-forward-step"></i>
          </button>
          <button class="text-lg text-lightest hover:text-white">
            <i class="fa-solid fa-repeat"></i>
          </button>
        </div>
        <div class="mt-2 flex items-center gap-2 w-full cursor-pointer">
          <span class="text-[10px] text-lightest">1:51</span>
          <div class="w-full h-1  bg-lightest rounded-full flex items-center ">
            <div class="bg-green h-1 w-[18%]"></div>
            <div class="h-3 w-3 rounded-full bg-white -ml-1 shadow-sm"></div>
          </div>
          <span class="text-[10px] text-lightest">5:50</span>
        </div>
      </div>
      <div class="flex items-center text-lightest gap-3 cursor-pointer ">
        <i class="fa-solid fa-microphone hover:text-white"></i>
        <i class="fa-solid fa-list hover:text-white"></i>
        <i class="fa-brands fa-chromecast hover:text-white "></i>
        <i class="fa-solid fa-volume-high hover:text-white"></i>
        <div class="w-20 bg-lightest -ml-2 rounded-full h-1 hover:text-white"></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      tabs: [
        { id: "home", name: "Home", icon: "fa-solid fa-house" },
        { id: "search", name: "Search", icon: "fa-solid fa-magnifying-glass" },
        { id: "library", name: "Your Library", icon: "bx bx-library" },
      ],
      id: "home",
      playlists: [
        { name: "The 1975 discography" },
        { name: "timeless" },
        { name: "'cause we all like to suffer'" },
        { name: "i have no idea why i love this" },
        { name: "lana del rey unreleased" },
        { name: "Summer Depression" },
        { name: "Taylor Swift Essential" },
        { name: "Romantizing heroine" },
        { name: "Taylor discography" },
      ],
      profile_dropdowns: [
        {
          id: "account",
          name: "Account",
          icon: "fa-solid fa-arrow-up-right-from-square",
        },
        { id: "profile", name: "Profile", icon: "" },
        {
          id: "premiun",
          name: "Upgrade to Premiun",
          icon: "fa-solid fa-arrow-up-right-from-square",
        },
        {
          id: "support",
          name: "Support",
          icon: "fa-solid fa-arrow-up-right-from-square",
        },
        {
          id: "download",
          name: "Download",
          icon: "fa-solid fa-arrow-up-right-from-square",
        },
        { id: "setting", name: "Setting", icon: "fa-solid fa-cog" },
      ],
      dropdown: false,
      recents: [
        { img: "lover.jpeg", title: "Lover", artist: " Taylor Swift" },
        {
          img: "ABIIOR.jpeg",
          title: "A Brief Inquiry ...",
          artist: " The 1975",
        },
        { img: "midnight.jpeg", title: "Midnights", artist: " Taylor Swift" },
        {
          img: "this_is_clairo.jpg",
          title: "This is Clairo",
          artist: "This is Clario. The essential tracks in a...",
        },
        { img: "NOACF.jpeg", title: "Note on A Con...", artist: "The 1975" },
      ],
      matty: [
        {
          img: "mix_1.jpeg",
          title: "Daily Mix 2",
          artist: "Taylor Swift, Halsey, Lorde and more.",
        },
        {
          img: "mix_2.jpeg",
          title: "Daily Mix 1",
          artist: "Billie Eilish, Lorde , Rina Sawayama, Bjork an...",
        },
        {
          img: "mix_3.jpeg",
          title: "Daily Mix 3",
          artist: "Doja Cat , Lady Gaga Ava Max and more.",
        },
        {
          img: "mix_5.jpeg",
          title: "Daily Mix 5",
          artist: "One Direction, The Wanted, Westlife, Backstreet Boy and...",
        },
        {
          img: "mix_6.jpeg",
          title: "Daily Mix 6",
          artist: "Madona, Adele, Dolly Parton and more.",
        },
      ],
      bests: [
        {
          img: "this_is_the_1975.jpeg",
          title: "This is The 1975",
          artist: "This is the 1975. The essential tracks in a..",
        },
        {
          img: "this_is_taylor_swift.jpeg",
          title: "This is The 1975",
          artist: "This is Taylor Swift. The essential tracks in al...",
        },
        {
          img: "this_is_harry_styles.jpg",
          title: "This is Harry Styles",
          artist: "This is Harry Styles. The essential tracks in a...",
        },
        {
          img: "lorde.jpg",
          title: "This is Lorde",
          artist: "This is Lorde. The essential tracks in all i..",
        },
        {
          img: "phoebe.jpg",
          title: "This is Phoebe Bri...",
          artist: "This is Phoebe Bridgers. The essential track i...",
        },
      ],
    };
  },
};
</script>
