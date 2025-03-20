<script lang="ts" setup>
const props = defineProps<{
    authorName?: string;
    desc?: string[];
    teamOf?: {name: string, link: string}[],
    contribution?: {name: string, link: string}[]
    avatar?: string;
}>();
</script>

<template>
    <div class="size-full flex items-center justify-center">
        <div class="max-w-xl w-full h-fit flex justify-center gap-16 mx-auto">
            <div class="w-md">
                <div>
                    <h1 class="text-white!">{{ props.authorName }}</h1>
                </div>
                <div class="opacity-80 leading-10" v-if="props.desc?.length">
                    <span v-for="desc of props.desc">{{ desc }} <br /> </span>
                </div>
                <div class="flex gap-2 items-center flex-wrap mt-2" v-if="props.teamOf && props.teamOf.length">
                    <span>组织:<br /></span>
                    <a v-for="team of props.teamOf" :href="team.link" class="no-underline! border-none! transition-all hover:text-white!">
                        <div class="px-2 py-1 rounded hover:bg-blue-600/20 hover:text-blue-200">
                            {{ team.name }}
                        </div>
                    </a>
                </div>
                <div class="flex gap-2 items-center flex-wrap mt-2" v-if="props.contribution && props.contribution.length">
                    <span>贡献者:<br /></span>
                    <a v-for="contribution of props.contribution" :href="contribution.link" class="no-underline! border-none! transition-all hover:text-white!">
                        <div class="px-2 py-1 rounded hover:bg-blue-600/20 hover:text-blue-200">
                            {{ contribution.name }}
                        </div>
                    </a>
                </div>
            </div>
            <div>
                <img :src="props.avatar" w-32 rounded-full />
            </div>
        </div>
    </div>
</template>