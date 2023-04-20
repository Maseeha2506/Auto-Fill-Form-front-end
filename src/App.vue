<template>
  <v-app>
    <v-navigation-drawer permanent fixed v-model="drawer" app color="#01579B" width="180" style="height:100vh;">
      <v-list-item class="px-2">
        <v-list-item-avatar>
          <v-img src="./assets/img.png"></v-img>
        </v-list-item-avatar>
        <v-list-item-title class="font-weight-black text-h6 white--text">DocVision</v-list-item-title>
      </v-list-item>
      <v-divider class="white--text"></v-divider>
      <v-list dense>
        <v-list-item v-for="item in items" :key="item.title" link :to="item.to">
          <v-list-item-icon>
            <v-icon :color="item.color">{{ item.icon }}</v-icon>
          </v-list-item-icon>
          <v-list-item-content>
            <v-list-item-title class="white--text">{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar flat app color="#01579B" dark> 
    </v-app-bar>
    <v-main>
      <router-view />
    </v-main>
  </v-app>
</template>
<script>
export default {
  data () {
    return {
       drawer: true,
        items: [
          { title: 'Image text extraction', icon: 'mdi-file-image', color:'#FFFFFF', to: '/orc' },
          { title: 'Form Recoginizer', icon: 'mdi-format-align-left', color: '#FFFFFF', to:'/orc1' },
        ],
        mini: true,
    }
    }
    }
</script>
