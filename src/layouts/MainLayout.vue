<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="leftDrawerOpen = !leftDrawerOpen"
        />
      </q-toolbar>
      <div class="q-px-lg q-pt-xl q-mb-md">
        <div class="text-h3">Todo</div>
        <div class="text-subtitle1">{{ todaysDate }}</div>
      </div>
      <q-img src="https://i.picsum.photos/id/0/5616/3744.jpg?hmac=3GAAioiQziMGEtLbfrdbcoenXoWAW-zlyEAMkfEdBzQ" class="header-image absolute-top" ></q-img>
    </q-header>

        <q-drawer
        v-model="leftDrawerOpen"
        show-if-above
        :width="300"
        :breakpoint="700"
      >
        <q-scroll-area style="height: calc(100% - 192px); margin-top: 192px; border-right: 1px solid #ddd">
          <q-list padding>
            <q-item to="/" clickable v-ripple>
              <q-item-section avatar>
                <q-icon name="list" color="accent" />
              </q-item-section>

              <q-item-section>
                ToDo
              </q-item-section>
            </q-item>

                    <q-item to="/help" clickable v-ripple>
              <q-item-section avatar>
                <q-icon name="help" color="accent"/>
              </q-item-section>

              <q-item-section>
                Help
              </q-item-section>
            </q-item>


          </q-list>
        </q-scroll-area>

        <q-img class="absolute-top"  src="https://i.picsum.photos/id/0/5616/3744.jpg?hmac=3GAAioiQziMGEtLbfrdbcoenXoWAW-zlyEAMkfEdBzQ" style="height: 150px">
          <div class="absolute-bottom bg-transparent">
            <q-avatar size="56px" class="q-mb-sm">
              <img src="https://cdn.quasar.dev/img/boy-avatar.png">
            </q-avatar>
            <div class="text-weight-bold">Vaughn Gigataras</div>
            <div>@vaughngigs</div>
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
import { date } from 'quasar'




export default {
  name: 'MainLayout',
  components: { },
  data () {
    return {
      leftDrawerOpen: false,
    }
  },
  computed: {
    todaysDate() {
      let timeStamp = Date.now()
      return date.formatDate(timeStamp, 'ddd, Do MMMM, YYYY HH:mm')
    }
  }
}
</script>

<style lang="scss">
.header-image {
  height: 100%;
  z-index: -1;
  opacity: 0.2;
  filter: greyscale(100%);

}
</style>
