<template>
  <div class="subject-wrapper">
    <div class="text-white mx-auto md:block hidden">
      <div class="shadow shadow-l"></div>
      <div class="shadow shadow-r"></div>
      <div class="subject-content flex-col flex items-center justify-center min-h-screen">
        <div class="flex items-center main-title">
          <div>{{ $t('main.title') }} </div>
          <span class="letter">&nbsp;</span>
          <div class="print-wrapper flex text-brand">
            <span v-for="(l, i) in printLetters" :key="i" class="letter" v-html="l"></span>
          </div>
        </div>
        <div class="mt-3 text-center sub-title animate__animated animate__fadeInDown animate__delay-1s">
          <p class="main-desc mb-6">
            {{ $t('main.subTitle') }}
          </p>
          <div class="flex items-center justify-center">
            <div class="feat-item flex items-center">
              <img class="h-[30px] w-[30px] rounded-full mr-1" src="@/assets/new-img/private.svg" alt="">
              {{ $t('main.private') }}
            </div>
            <div class="w-2 h-2 rounded bg-white mx-8"></div>

            <div class="feat-item flex items-center">
              <img class="h-[30px] w-[30px] rounded-full mr-1" src="@/assets/new-img/secure.svg" alt="">

              {{ $t('main.secure') }}
            </div>
            <div class="w-2 h-2 rounded bg-white mx-8"></div>

            <div class="feat-item flex items-center">
              <img class="h-[30px] w-[30px] rounded-full mr-1" src="@/assets/new-img/decentralized.svg" alt="">

              {{ $t('main.decentralized') }}
            </div>
            <div class="w-2 h-2 rounded bg-white mx-8"></div>

            <div class="feat-item flex items-center">
              <img class="h-[30px] w-[30px] rounded-full mr-1" src="@/assets/new-img/versatile.svg" alt="">
              {{ $t('main.versatile') }}
            </div>
          </div>
        </div>
        <div class="text-center mt-20">
          <NewDownload />
        </div>
      </div>
    </div>
    <div class="md:hidden block text-white text-center px-5 pt-20">
      <div class="shadow-m shadow-m-l"></div>
      <div class="shadow-m shadow-m-r"></div>
      <div class="flex flex-col main-title-m">
        <div>{{ $t('main.title') }} </div>
        <div class="print-wrapper print-wrapper-m flex text-brand">
          <span v-for="(l, i) in printLetters" :key="i" class="letter" v-html="l"></span>
        </div>
      </div>
      <div class="mt-3 text-center sub-title animate__animated animate__fadeInDown animate__delay-1s">
        <p class="main-desc-m mb-2">
          {{ $t('main.subTitle') }}
        </p>
        <div class="flex items-center justify-center">
          <div class="feat-mobile-item flex items-center">
            <img class="h-[24px] w-[24px] rounded-full mr-1" src="@/assets/new-img/private.svg" alt="">
            {{ $t('main.private') }}
          </div>

          <div class="w-2 h-2 rounded bg-white mx-3"></div>

          <div class="feat-mobile-item flex items-center">
            <img class="h-[24px] w-[24px] rounded-full mr-1" src="@/assets/new-img/secure.svg" alt="">
            {{ $t('main.secure') }}
          </div>
        </div>
        <div class="flex items-center justify-center">
          <div class="feat-mobile-item flex items-center">
            <img class="h-[24px] w-[24px] rounded-full mr-1" src="@/assets/new-img/decentralized.svg" alt="">
            {{ $t('main.decentralized') }}
          </div>

          <div class="w-2 h-2 rounded bg-white mx-3"></div>

          <div class="feat-mobile-item flex items-center">
            <img class="h-[24px] w-[24px] rounded-full mr-1" src="@/assets/new-img/versatile.svg" alt="">
            {{ $t('main.versatile') }}
          </div>
        </div>
      </div>
      <div class="text-center mt-20">
        <NewDownload />
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      letters: ['W', 'e', 'b', '3', '&nbsp;', 'W', 'a', 'l', 'l', 'e', 't'],
      zhLetters: ['W', 'e', 'b', '3', '&nbsp;', '钱', '包'],
      printLetters: [],
      interval: null,
      count: 0,
    }
  },
  mounted() {
    this.print()
  },
  beforeUnmount() {
    clearInterval(this.interval)
  },
  methods: {
    print() {
      this.printLetters = []
      this.count = 0
      let originTitle = []
      if (this.$i18n.locale === 'en') {
        originTitle = this.letters
      } else {
        originTitle = this.zhLetters
      }
      this.interval = setInterval(() => {
        if (this.count > originTitle.length - 1) {
          clearInterval(this.interval)
          setTimeout(() => {
            this.print()
          }, 4000)
        }
        this.printLetters.push(originTitle[this.count++])
      }, 150)
    },
    download(platform) {
      this.$emit('download', platform)
    }
  }
}
</script>
<style scoped>
.print-wrapper-m {
  margin: 0 auto;
  height: 75px;
}

.print-wrapper {
  animation: blink-caret 0.75s step-end infinite;
}

@keyframes blink-caret {

  from,
  to {
    box-shadow: 1px 0 0 0 transparent;
  }

  50% {
    box-shadow: 1px 0px 0 0;
  }
}

.subject-wrapper {
  position: relative;
}

.subject-content {
  z-index: 1;
}

.main-title {
  font-family: 'Poppins-Bold';
  font-size: 100px;
  line-height: 150px;
  font-weight: 700;
}

.main-title-m {
  font-family: 'Poppins-Bold';
  font-size: 50px;
  line-height: 75px;
  font-weight: 700;
}

.sub-title {
  font-size: 26px;
  line-height: 39px;
  font-weight: 400;
}

.main-desc {
  font-size: 40px;
}
.main-desc-m {
  font-size: 24px;
}
.download-wrapper {
  width: 100%;
  display: flex;
  align-items: center;
}

.shadow {
  background: rgba(18, 254, 116, 0.9);
  opacity: .3;
  filter: blur(150px);
  height: 637px;
  width: 637px;
  border-radius: 100%;
  z-index: 1;
}

.shadow-l {
  position: absolute;
  left: -220px;
  top: 0;
}

.shadow-r {
  position: absolute;
  right: -220px;
  bottom: -400px;
}

.shadow-m {
  background: rgba(18, 254, 116, 0.9);
  opacity: .3;
  filter: blur(30px);
  height: 283px;
  width: 283px;
  border-radius: 100%;
  z-index: 1;
}

.shadow-m-l {
  position: absolute;
  left: -122px;
  top: 0;
}

.shadow-m-r {
  position: absolute;
  right: -122px;
  bottom: 0px;
}

.feat-item {
  font-size: 24px;

  img {
    height: 30px;
    width: 30px;
  }
}

.feat-mobile-item {
  font-size: 16px;

  img {
    height: 24px;
    width: 24px;
  }
}
</style>
