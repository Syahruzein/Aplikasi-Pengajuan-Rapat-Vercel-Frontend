<template>
    <v-app light>
    <v-navigation-drawer
      v-model="drawer"
      :mini-variant="miniVariant"
      :clipped="clipped"
      fixed
      app
      class="borderRight"
    >
      <v-list>
        <v-list-item
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          router
          exact
        >
          <v-list-item-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title v-text="item.title" />
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar
      :clipped-left="clipped"
      fixed
      app
    >
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-btn
        icon
        @click.stop="miniVariant = !miniVariant"
      >
        <v-icon>mdi-{{ `chevron-${miniVariant ? 'right' : 'left'}` }}</v-icon>
      </v-btn>
      <v-btn
        icon
        @click.stop="clipped = !clipped"
      >
        <v-icon>mdi-application</v-icon>
      </v-btn>
      <v-btn
        icon
        @click.stop="fixed = !fixed"
      >
        <v-icon>mdi-minus</v-icon>
      </v-btn>
      <v-toolbar-title v-text="title" />
      <v-spacer />
    </v-app-bar>
    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
    <v-footer
      :absolute="!fixed"
      app
      class="justify-end"
    >
      <span class="text--secondary">Website Pengajuan Rapat PENS &copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>
<script>
export default {
    name: 'users',
    data () {
        return {
        clipped: false,
        drawer: true,
        fixed: false,
        items: [
            {
            icon: 'mdi-home',
            title: 'Beranda',
            to: '/user/users/Beranda'
            },
            {
            icon: 'mdi-receipt-text-plus',
            title: 'Pengajuan Rapat',
            to: '/user/users/Pengajuan'
            },
            {
            icon: 'mdi-database',
            title: 'Data Pengajuan',
            to: '/user/users/DataPengajuan'
            },
            {
            icon: 'mdi-calendar-month',
            title: 'Jadwal Rapat',
            to: '/user/users/Jadwal'
            },
            {
            icon: 'mdi-note-text',
            title: 'Notulen Rapat',
            to: '/user/users/Notulen'
            }
        ],
        miniVariant: false,
        title: 'Aplikasi Pengajuan Rapat'
        }
    }
}
</script>
<style>
    
</style>