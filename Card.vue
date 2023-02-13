<template>
    <div class="container p-px mx-auto h-full">
        <div :class="statusObj" class="border-t-8 w-4/5 bg-white mx-auto mt-4 border-gray-100 shadow p-5 rounded-md">
            <!-- <div class="flex justify-center">
                <img class="w-2/3 py-6" :src="imgStatus" alt="">
            </div> -->
            <h2 class="font-semibold text-2xl">
                {{name}}
                <span :class="typeObj" class="inline-block p-1 font-medium text-sm rounded-md">{{ type }}</span>
            </h2>
            <h3 class="font-medium text-xl mb-2 text-gray-500">{{ subName }}</h3>
            <div class="break-words" v-for="description in descriptions">
                    <p>{{description}}</p>
            </div>
            <hr class="m-2" />
            <p class="">結果： <span class="font-medium">{{ status }}</span></p>
            <p class="text-slate-500">{{ note }}</p>
        </div>
    </div>
</template>

<script>
const statusColor = {
    "表決不通過": "border-t-red-500",
    "照案通過": "border-t-green-500",
    "無須表決": "border-t-gray-500",
    "部分條文通過": "border-t-yellow-500",
    "擱置": "border-t-amber-500",
    "緩議": "border-t-amber-500",
}

const typeColor = {
    "決議案": "bg-blue-900 text-blue-100",
    "法規修正案": "bg-cyan-900 text-cyan-100",
    "程序性動議": "bg-gray-200",
    "意見陳述": "bg-gray-200 text-gray-800", 
}

export default {
    name: 'card',
    props: ['name','subName','type','status', 'note','pDescription'],
    data: () => {
        return {

        }
    },
    computed: {
        statusObj() {
            return this.status ? {
                [statusColor[this.status]]: true,
            } : {
                'border-t-slate-400': true
            }
        },
        typeObj() {
            return {
                [typeColor[this.type]]: true,
            }
        },
        imgStatus() {
            return `/imgs/${this.status}.png`
        },
        descriptions() {
            return this.pDescription.split('\n')
        }
    }
}
</script>
