<script lang="ts" setup>
import { computed, Ref } from 'vue';
const P=0;
const showNuxt = computed(() => $clicks.value >= P+1)
const showVue = computed(() => $clicks.value >= P+2)
const showTS = computed(() => $clicks.value >= P+3)
const showVite = computed(() => $clicks.value >= P+4)

const isVite = computed(() => $clicks.value === P+4)
const isWebpack = computed(() => $clicks.value === P+5)
const isRspack = computed(() => $clicks.value === P+6)
const isFarm = computed(() => $clicks.value === P+7)

</script>

<template>
    <div size-full flex items-center>
        <div w-xxl mx-auto flex gap-16 items-center mb-20 transition-all>
            <transition-group name="scale">
                <div class="shrink-0 size-20" v-if="showNuxt" key="nuxt">
                    <img src="/images/nest-js.png" size-20 />
                </div>
                <div class="shrink-0 size-25" v-if="showVue" key="vue">
                    <img src="/images/vue.png" size-25 />
                </div>
                <div class="shrink-0 size-20" v-if="showTS" key="ts">
                    <img src="/images/ts-logo-512.png" size-20 />
                </div>
                <div class="relative overflow-hidden shrink-0 wrapper" v-if="showVite" key="vite">
                    <transition name="fade-slide-top" mode="out-in">
                        <img key="vite" src="/images/vite.png" size-20 v-if="isVite" />
                        <img key="webpack" src="/images/webpack.png" size-20 v-else-if="isWebpack" />
                        <img key="rspack" src="/images/rspack.png" size-20 v-else-if="isRspack" />
                        <img key="farm" src="/images/farm.png" w-40 v-else-if="isFarm" />
                    </transition>
                </div>
            </transition-group>
        </div>
    </div>
</template>

<style>
.wrapper {
    mask-image: linear-gradient(#000,#000,transparent 0,#000 5px,#000 calc(100% - 5px),transparent);
}
.fade-slide-top-enter-active,
.fade-slide-top-leave-active{
    transition: all .3s ease-in-out;
}

.fade-slide-top-enter-to,
.fade-slide-top-leave-from {
  transform: translateY(0px);
  opacity: 1;
}

.fade-slide-top-enter-from {
    transform: translateY(20px);
    opacity: 0;
}

.fade-slide-top-leave-to {
  transform: translateY(-20px);
  opacity: 0;
}

.scale-enter-active,
.scale-move{
  transition: all 0.3s ease-in-out;
}

.scale-leave-active {
  transition: all 0.3s ease-in-out;
}

.scale-enter-from,
.scale-leave-to {
  transform: scale(0);
  filter: blur(10px);
  opacity: 0;
}
</style>