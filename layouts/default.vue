<template>
  <div id="app">
    <v-app>
      <v-app-bar fixed max-height="64px">
        <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>
        <div class="nav-main">
          <v-btn plain to="/" class="nav-item">
            <h1>米亞MYA</h1>
          </v-btn>
          <span class="d-md-flex d-none ml-3" v-if="showCelebrate">
            <v-icon class="mr-2">{{ mdiPartyPopper }}</v-icon>
            <p class="text-h6">恭喜米亞{{ status.subscriberCount }}訂閱!!</p>
          </span>
        </div>
        <v-spacer />
        <v-btn plain v-if="showSnow && snowflakes != null" class="d-none d-md-block" @click="toggleSnow">
          Hide Snow
        </v-btn>
        <v-btn plain v-else-if="showSnow" class="d-none d-md-block" @click="toggleSnow">
          Show Snow
        </v-btn>
        <v-btn plain class="d-none d-md-block" v-if="!$vuetify.theme.current.dark" @click="toggleTheme(false)">
          Darkmode
        </v-btn>
        <v-btn class="d-none d-md-block" v-else plain @click="toggleTheme(false)">
          Lightmode
        </v-btn>
      </v-app-bar>
      <v-navigation-drawer v-model="drawer" class="text-left" temporary fixed>
        <v-list-item class="my-3">
          <v-list-item-title class="text-h5"> 米亞MYA </v-list-item-title>
          <v-list-item-subtitle> 一名來自香港的VTuber </v-list-item-subtitle>
        </v-list-item>
        <v-list nav dense>
          <v-list-item to="/" link>
            <template v-slot:prepend>
              <v-icon>{{ mdiHome }}</v-icon>
            </template>
            <v-list-item-title>米亞</v-list-item-title>
          </v-list-item>
          <v-list-item to="/gummy" link>
            <template v-slot:prepend>
              <v-icon>{{ mdiAccount }}</v-icon>
            </template>
            <v-list-item-title>甘米主人</v-list-item-title>
          </v-list-item>

          <v-list-item to="/teahouse" link>
            <template v-slot:prepend>
              <v-icon>{{ mdiCoffee }}</v-icon>
            </template>
            <v-list-item-title>幻花茶屋</v-list-item-title>
          </v-list-item>

          <v-list-item to="/mya-meme" link>
            <template v-slot:prepend>
              <v-icon>{{ mdiBook }}</v-icon>
            </template>
            <v-list-item-title>米亞梗字典</v-list-item-title>
          </v-list-item>

          <v-list-item to="/achievement" link>
            <template v-slot:prepend>
              <v-icon>{{ mdiTrophy }}</v-icon>
            </template>
            <v-list-item-title>路程杯</v-list-item-title>
          </v-list-item>

          <v-list-item to="/adventure" link>
            <template v-slot:prepend>
              <v-icon>{{ mdiBook }}</v-icon>
            </template>
            <v-list-item-title>頂米亞大冒險</v-list-item-title>
          </v-list-item>

          <v-list-item to="/bbq" link>
            <template v-slot:prepend>
              <v-icon>{{ mdiFoodDrumstick }}</v-icon>
            </template>
            <v-list-item-title>米亞烤肉</v-list-item-title>
          </v-list-item>

          <v-list-item to="/mya" link>
            <template v-slot:prepend>
              <v-icon>
                <YoutubeIcon size="20" />
              </v-icon>
            </template>
            <v-list-item-title>米亞過往的影片</v-list-item-title>
          </v-list-item>

          <v-list-item to="/games" link>
            <template v-slot:prepend>
              <v-icon>
                {{ mdiController }}
              </v-icon>
            </template>
            <v-list-item-title>院友自製遊戲</v-list-item-title>
          </v-list-item>
          <v-list-item to="/thanks" link>
            <template v-slot:prepend>
              <v-icon>{{ mdiPartyPopper }}</v-icon>
            </template>
            <v-list-item-title>特別感謝</v-list-item-title>
          </v-list-item>

          <v-divider></v-divider>
          <v-list-item :ripple="false" disabled>
            <v-list-item-title> 米亞の外部鏈接 </v-list-item-title>
          </v-list-item>
          <v-divider></v-divider>
          <v-list-item target="_blank" href="https://www.youtube.com/channel/UCVDrzfo7NnOvNx8dU-Ebitg" link>
            <ClientOnly>
              <YoutubeIcon size="20" />
            </ClientOnly>
            <v-list-item-title>Youtube</v-list-item-title>
          </v-list-item>

          <v-list-item href="https://twitter.com/MyaVtuber" target="_blank" link>
            <ClientOnly>
              <TwitterIcon size="20" />
            </ClientOnly>

            <v-list-item-title>Twitter</v-list-item-title>
          </v-list-item>

          <v-list-item href="https://www.instagram.com/mya_vtuber/" target="_blank" link>
            <ClientOnly>
              <InstagramIcon size="20" />
            </ClientOnly>

            <v-list-item-title>Instagram</v-list-item-title>
          </v-list-item>

          <v-list-item target="_blank" href="https://www.facebook.com/myavtuber" link>
            <ClientOnly>
              <FacebookIcon size="20" />
            </ClientOnly>
            <v-list-item-title>Facebook</v-list-item-title>
          </v-list-item>
          <v-list-item href="https://discord.com/invite/erB5AW9Vrp" target="_blank" link>
            <ClientOnly>
              <DiscordIcon size="20" />
            </ClientOnly>
            <v-list-item-title>Discord</v-list-item-title>
          </v-list-item>
          <v-list-item href="https://minecraft.mya-hkvtuber.com/" target="_blank" link>
            <ClientOnly>
              <MinecraftIcon size="20" />
            </ClientOnly>
            <v-list-item-title>Minecraft</v-list-item-title>
          </v-list-item>
          <v-divider class="d-md-none mt-5"></v-divider>
          <div class="d-md-none pt-3">
            <v-btn plain block v-if="!$vuetify.theme.current.dark" @click="$vuetify.theme.current.dark = true">
              Darkmode
            </v-btn>
            <v-btn v-else plain block @click="$vuetify.theme.current.dark = false">
              Lightmode
            </v-btn>
          </div>
        </v-list>
      </v-navigation-drawer>
      <v-main class="pt-15">
        <slot></slot>
        <v-dialog v-if="specialCelebrate.showSpecialModel" v-model="specialCelebrate.showSpecialModel" max-width="500">
          <v-card>
            <v-card-title> 米亞再次達成突破性路程杯啦！！ </v-card-title>
            <v-card-text>
              <span class="d-md-flex d-none" v-if="specialCelebrate.showSpecialCelebrate">
                <v-icon class="mr-2">{{ mdiPartyPopper }}</v-icon>
                <p class="text-h6">
                  {{ specialCelebrate.specialCelebrateText }}
                </p>
                <v-icon class="mr-2">{{ mdiPartyPopper }}</v-icon>
              </span>
            </v-card-text>
            <v-card-actions class="justify-space-between">
              <v-btn color="red" class="w-50" @click="specialCelebrate.showSpecialModel = false">
                關閉
              </v-btn>
              <v-btn color="pink" class="w-50" to="/celebrate3Dsuccess"
                @click="specialCelebrate.showSpecialModel = false">
                精彩彩蛋
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-main>
      <v-footer app class="px-md-15" absolute>
        <p class="mb-0 py-5 footer">
          Crafted By <a href="https://github.com/PoH98">PoH98</a>,
          <a href="https://github.com/sawaYch">Sawa</a>
        </p>
        <v-spacer />
        <div class="footer">
          Copyright MIT License<br /><a href="https://github.com/PoH98/MyaVTuber-Site">Github Source Code</a>
        </div>
      </v-footer>
    </v-app>
  </div>
  <canvas id="live2d" ref="vue-live2d-main" :width="250" :height="250" class="vue-live2d-main"></canvas>
</template>
<script>
import { useSharedDataStore } from '@/store/sharedData.js';
import { useThemeStore } from '@/store/themeStore';
import { useTheme } from 'vuetify';
import Snowflakes from 'magic-snowflakes';
import { TwitterIcon, DiscordIcon, InstagramIcon, YoutubeIcon, FacebookIcon, MinecraftIcon } from 'vue3-simple-icons'
import {
  mdiMinecraft,
  mdiAccount,
  mdiCoffee,
  mdiHome,
  mdiController,
  mdiFoodDrumstick,
  mdiPartyPopper,
  mdiTrophy,
  mdiBook,
} from "@mdi/js";
import config from "@/plugins/specialEvent.json";
export default {
  name: "defaultLayout",
  components: {
    YoutubeIcon,
    TwitterIcon,
    DiscordIcon,
    InstagramIcon,
    FacebookIcon,
    MinecraftIcon
  },
  setup() {
    const theme = useTheme()
    const store = useSharedDataStore();
    const themeStore = useThemeStore();
    return {
      store,
      theme,
      themeStore,
      toggleTheme: (avoidStore) => {
        const t = theme.global.current.value.dark ? 'light' : 'dark';
        if (!avoidStore) {
          themeStore.theme = t;
          console.log(themeStore.theme);
        }
        theme.global.name.value = t;
      }
    }
  },
  data() {
    return {
      drawer: false,
      mdiMinecraft,
      mdiAccount,
      mdiCoffee,
      mdiHome,
      mdiController,
      mdiFoodDrumstick,
      mdiPartyPopper,
      mdiBook,
      mdiTrophy,
      celebrate: [
        10000, 20000, 30000, 40000, 50000, 60000, 70000, 80000, 90000, 100000,
        200000, 3000000, 400000, 5000000, 600000, 700000, 800000, 900000,
        1000000,
      ],
      showCelebrate: false,
      specialCelebrate: {},
      showSnow: false,
      snowflakes: null
    };
  },
  computed: {
    status() {
      return this.store.status;
    },
  },
  watch: {
    $route() {
      const event = new Event("changePage");
      document.dispatchEvent(event);
    },
  },
  methods: {
    toggleSnow() {
      if (this.snowflakes == null) {
        this.snowflakes = new Snowflakes({
          color: '#ccc',
          count: 20,
          minSize: 10,
          maxSize: 15
        });
        this.snowflakes.start();
        localStorage.setItem("disableSnow", "");
      }
      else {
        this.snowflakes?.stop();
        this.snowflakes?.destroy();
        this.snowflakes = null;
        localStorage.setItem("disableSnow", "true")
      }

    },
    async specialEvents() {
      const month = new Date().getMonth() + 1;
      //subscribers celebrate or mya birthday celebrate
      if (!document.getElementById("confetti-canvas")) {
        if (this.celebrate.includes(parseInt(this.status.subscriberCount))) {
          this.showCelebrate = true;
          const VueConfetti = await import("vue-confetti");
          this.$confetti = new VueConfetti.Confetti();
          if (window.innerWidth > 480) {
            this.$confetti.start({
              defaultSize: 5,
              particlesPerFrame: 0.1,
              windSpeedMax: 0,
              defaultDropRate: 2,
            });
          } else {
            this.$confetti.start({
              defaultSize: 5,
              particlesPerFrame: 0.05,
              windSpeedMax: 0,
              defaultDropRate: 2,
            });
          }
        }
        if (this.specialCelebrate.showSpecialCelebrate) {
          if (this.$route.name !== "celebrate3Dsuccess") {
            this.specialCelebrate.showSpecialModel = true;
          }
          const VueConfetti = await import("vue-confetti");
          this.$confetti = new VueConfetti.Confetti();
          if (window.innerWidth > 480) {
            this.$confetti.start({
              defaultSize: 5,
              particlesPerFrame: 0.1,
              windSpeedMax: 0,
              defaultDropRate: 2,
            });
          } else {
            this.$confetti.start({
              defaultSize: 5,
              particlesPerFrame: 0.05,
              windSpeedMax: 0,
              defaultDropRate: 2,
            });
          }
        }
      }
      // month will reduce 1 at here so we add 1 for real world month
      if (process.client)
        this.showSnow = true;
      if ((month <= 2 || month == 12) && localStorage.getItem("disableSnow") != "true") {
        this.snowflakes = new Snowflakes({
          color: '#ccc',
          count: 20,
          minSize: 10,
          maxSize: 15
        });
        this.snowflakes.start();
      }
    }
  },
  beforeMount() {
    this.specialCelebrate = config;
  },
  async mounted() {
    if (this.themeStore.theme === 'dark') {
      setTimeout(() => {
        this.toggleTheme(true);
      }, 100)
    }
    else if (this.themeStore.theme === null) {
      if (
        window.matchMedia &&
        window.matchMedia("(prefers-color-scheme: dark)").matches
      ) {
        this.toggleTheme(false);
      }
    }

    window.addEventListener("auxclick", (event) => {
      if (event.button === 1) event.preventDefault();
    });
    await this.store.fetchYTData();
    if (process.client) {
      await this.specialEvents();
    }
  },
};
</script>
<style scoped lang="scss">
.vue-live2d-main {
  position: fixed;
  z-index: 1010;
  pointer-events: none;
}

.nav-item {
  margin-left: 5px;
  margin-right: 5px;
}

.footer {
  font-size: 10px;
}


@media (min-width: 720px) {
  .nav-item {
    min-width: 100px !important;
  }
}

@media (max-width: 480px) {
  .nav-main {
    min-width: 80%;
    align-items: center;
    display: flex;
  }

  .nav-main .home {
    min-width: 100% !important;
  }
}
</style>
<style lang="scss">
:global {
  @font-face {
    font-family: 'Yuanti TC';
    src: url('/fonts/STYuanti-TC-Bold.woff2') format('woff2'), url('/fonts/STYuanti-TC-Bold.woff') format('woff');
    font-weight: normal;
    font-style: normal;
    font-display: swap;
  }
}

body {
  max-width: 100vw;
}

#confetti-canvas {
  z-index: 1;
}

@media (min-width: 1920px) {
  .v-container {
    max-width: 1280px
  }
}

@media (min-width: 2560px) {
  .v-container {
    max-width: 1920px
  }
}

#app {
  font-family: "Yuanti TC" !important;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  overflow-x: hidden;
  max-width: 100vw;
  user-select: none;
  font-size: 14px;

  .v-navigation-drawer .v-list-item__content {
    display: flex;
    align-items: center;
    flex-wrap: wrap;

    >i {
      margin-right: 12px;
    }

    >svg {
      margin-right: 12px;
    }

    .v-list-item-title {
      flex: 0 0 auto;
      max-width: 100%;
    }

    .v-list-item-subtitle {
      flex: 0 0 100%;
      max-width: 100%;
    }
  }

  p {
    margin-bottom: 0;
  }

  path {
    fill: currentColor;
  }

  @media (min-width: 1904px) {
    .container {
      max-width: 1185px !important;
    }
  }

  .home {
    border: 3px solid currentColor !important;
    padding: 10px 32px !important;
  }

  .home * {
    font-size: 30px;
  }

  .home:before {
    background-color: white !important;
  }

  .img-fluid {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }

  #gummy-vid {
    top: -55px;
    left: -10px;
    right: 0;
    width: calc(100% + 20px);
    min-height: 100%;
    opacity: 1;
  }

  /* ===== Scrollbar CSS ===== */
  /* Firefox */
  * {
    scrollbar-width: thin;
    scrollbar-color: #ff00bb #ffffff;
  }

  /* Chrome, Edge, and Safari */
  *::-webkit-scrollbar {
    width: 14px;
  }

  *::-webkit-scrollbar-track {
    background: #ffffff;
  }

  *::-webkit-scrollbar-thumb {
    background-color: #ff00bb;
    border-radius: 10px;
    border: 3px solid #ffffff;
  }

  .theme--dark.v-sheet a {
    color: white;
  }

  .nav-item.v-btn--active>.v-btn__overlay {
    opacity: 0;
  }

  h1,
  h2,
  h3,
  h4,
  h5,
  h6 {
    -webkit-text-stroke-width: .6px;
    -webkit-text-stroke-color: #ddd;
    -webkit-text-fill-color: #f27386;
    paint-order: stroke fill;
    text-shadow: 1px 2px 4px rgba(0, 0, 0, 0.3);
  }
}

.w-50 {
  width: 49%;
}

.PhotoConsumer {
  width: 100%;
}
</style>
