<template>
    <div v-if="data.length > 0">
        <v-card
            v-for="i in data"
            class="my-4"
            @click="
                $router.push({
                    name: 'TeamListPage',
                    params: {
                        roomId: i.id,
                    },
                })
            "
        >
            <v-card-title>{{ i.data.roomName }}</v-card-title>
            <v-card-text>
                <div class="d-flex" style="overflow-x: hidden">
                    <span class="d-flex" v-for="(n, nIndex) in i.data.allTeam">
                        {{ n.member.join(' , ') }}
                    </span>
                </div>
            </v-card-text>
        </v-card>
    </div>
    <div v-else>NoData</div>
</template>
<script setup lang="ts">
import { onMounted } from 'vue'
import { ref } from 'vue'
const data = ref<any>([])
onMounted(async () => {
    data.value = await fetch('https://bad-boy-service.vercel.app/room').then(
        (e) => e.json()
    )
})
</script>
