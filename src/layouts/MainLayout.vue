<template>
    <q-layout view="lHh Lpr lFf">
        <q-header>
            <q-toolbar>
                <q-btn
                    flat
                    dense
                    round
                    icon="menu"
                    aria-label="Menu"
                    @click="toggleLeftDrawer"
                />
            </q-toolbar>
            <div class="q-px-lg q-pt-xl q-mb-md">
                <div class="text-h3">Todo</div>
                <div class="text-subtitle">{{ todayDate }}</div>
            </div>
            <img src="../assets/tree.jpg" class="header-image absolute-top" />
        </q-header>

        <q-drawer v-model="drawer" show-if-above :width="250" :breakpoint="600">
            <q-scroll-area
                style="
                    height: calc(100% - 185px);
                    margin-top: 185px;
                    border-right: 1px solid #ddd;
                "
            >
                <q-list padding>
                    <q-item to="/" exact clickable v-ripple>
                        <q-item-section avatar>
                            <q-icon name="list" />
                        </q-item-section>
                        <q-item-section> Todo </q-item-section>
                    </q-item>
                    <q-item to="/help" exact clickable v-ripple>
                        <q-item-section avatar>
                            <q-icon name="help" />
                        </q-item-section>
                        <q-item-section> Help </q-item-section>
                    </q-item>
                </q-list>
            </q-scroll-area>

            <q-img
                class="absolute-top"
                src="../assets/tree.jpg"
                style="height: 185px"
            >
                <div class="absolute-bottom bg-transparent">
                    <q-avatar size="56px" class="q-mb-sm">
                        <img src="https://cdn.quasar.dev/img/boy-avatar.png" />
                    </q-avatar>
                    <div class="text-weight-bold">Pham Quang Tung</div>
                    <div>@tungpham</div>
                </div>
            </q-img>
        </q-drawer>

        <q-page-container>
            <keep-alive>
                <router-view />
            </keep-alive>
        </q-page-container>
    </q-layout>
</template>

<script>
import { date } from "quasar";
import { defineComponent, ref } from "vue";
import EssentialLink from "components/EssentialLink.vue";

const linksList = [
    {
        title: "Docs",
        caption: "quasar.dev",
        icon: "school",
        link: "https://quasar.dev",
    },
    {
        title: "Github",
        caption: "github.com/quasarframework",
        icon: "code",
        link: "https://github.com/quasarframework",
    },
];

export default defineComponent({
    name: "MainLayout",

    components: {
        EssentialLink,
    },

    setup() {
        const leftDrawerOpen = ref(false);

        return {
            essentialLinks: linksList,
            leftDrawerOpen,
            toggleLeftDrawer() {
                leftDrawerOpen.value = !leftDrawerOpen.value;
            },
        };
    },
    computed: {
        todayDate() {
            const timeStamp = Date.now();
            const formattedString = date.formatDate(timeStamp, "D MMMM YYYY");
            return formattedString;
        },
    },
});
</script>
<style lang="scss">
.header-image {
    height: 100%;
    width: 100%;
    z-index: -1;
    opacity: 0.2;
    filter: grayscale(100%);
}
</style>>