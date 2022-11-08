<template>
  <q-layout view="lHh Lpr lFf">
    <q-header >
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
        <div class="text-h3"> Cosas por hacer</div>
        <div class="text-subtitle1">{{ formattedString }}</div>

      </div>
      <q-img
        src="../assets/icons/beach.jpg"
        class="header-image absolute-top"
      />


    </q-header>

    <q-drawer
        v-model="leftDrawerOpen"
        show-if-above
        :width="250"
        :breakpoint="600"
      >
        <q-scroll-area style="height: calc(100% - 192px); margin-top: 192px; border-right: 1px solid #ddd">
          <q-list padding>
            <q-item to="/"
              exact
              clickable v-ripple>
              <q-item-section avatar>
                <q-icon name="list" />
              </q-item-section>
              <q-item-section>
                Lista
              </q-item-section>
            </q-item>

            <q-item to="/help"
              exact
              clickable v-ripple>
              <q-item-section avatar>
                <q-icon name="help" />
              </q-item-section>
              <q-item-section>
                Ayuda
              </q-item-section>
            </q-item>
          </q-list>
        </q-scroll-area>

        <q-img class="absolute-top" src="../assets/icons/beach.jpg" style="height: 192px">
          <div class="absolute-bottom bg-transparent">
            <q-avatar size="56px" class="q-mb-sm">
              <img src="../assets/icons/arbiter.jpg">
            </q-avatar>
            <div class="text-weight-bold">Cachichurris</div>
            <div>@cachichurris</div>
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

<script setup lang="ts">
import { date } from 'quasar'
import { ref } from 'vue';
import EssentialLink, { EssentialLinkProps } from 'components/EssentialLink.vue';

const timeStamp = Date.now()
const formattedString = date.formatDate(timeStamp, 'dddd D MMMM ')




const leftDrawerOpen = ref(false)

function toggleLeftDrawer() {
  leftDrawerOpen.value = !leftDrawerOpen.value
}
</script>


<style lang="scss">
  .header-image {
    height: 100%;
    z-index: -1;
    width: 100%;
    opacity: 0.2;
    filter: grayscale(100%);
  }
</style>
