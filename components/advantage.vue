<script lang="ts" setup>
const datas = [
    { title: '细颗粒度权限管理', img: '细颗粒度权限管理.png' },
    { title: '多种布局', img: '多种布局.png'},
    { title: '多种主题', img: '多种主题.png'},
    { title: '国际化', img: '国际化.png'},
    { title: '可视化创建国际化', img: '可视化创建国际化.png'},
    { title: '可视化绑定菜单', img: '可视化绑定菜单.png'},
    { title: '可视化创建菜单', img: '可视化创建菜单.png'},
    { title: '可视化角色管理', img: '角色管理.png'},
]
</script>

<template>
    <div class="w-full h-fit mt-4 flex flex-col items-center justify-center gap-2 overflow-hidden">
        <div class="w-full h-[350px]">
            <transition name="fade-slide-top" mode="out-in">
                <img :key="$clicks" :src="`/images/${datas[$clicks].img}`" alt="" class="h-full mx-auto" />
            </transition>
        </div>
        <transition name="fade-slide-top" mode="out-in">
            <span :key="$clicks" class="h-fit shrink-0">{{ datas[$clicks].title }}</span>
        </transition>
    </div>
</template>

<style scoped>
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
</style>