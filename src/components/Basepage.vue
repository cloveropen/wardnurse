<template>
  <div>
    <v-navigation-drawer
      v-model="drawer"
      :clipped="$vuetify.breakpoint.lgAndUp"
      app
    >
    <v-flex d-flex>
              &emsp;&emsp;
              <v-select
                v-model="room"
                :items="depts"
                item-text="item-text"
                item-value="item-value"
                label="病区"
                hide-details
                prepend-icon="map"
              ></v-select>
            </v-flex>
<v-flex d-flex>
             &nbsp; 病情            
             <v-checkbox v-model="checkbox1" label="一般"></v-checkbox>&nbsp;
    <v-checkbox v-model="checkbox2" label="急"></v-checkbox>&nbsp;
    <v-checkbox v-model="checkbox3" label="重"></v-checkbox>
</v-flex>
      <v-expansion-panels popout>
        <v-expansion-panel>
          <v-expansion-panel-header>住院患者列表</v-expansion-panel-header>
          <v-expansion-panel-content>
            <v-card>
              <v-card-title>
                <v-text-field
                  v-model="search"
                  append-icon="search"
                  label="姓名或住院号"
                  single-line
                  hide-details
                ></v-text-field>
              </v-card-title>
              <v-data-table
                :headers="headers"
                :items="desserts"
                :search="search" @click:row="getpatient($event)"
              ></v-data-table>
            </v-card>
          </v-expansion-panel-content>
        </v-expansion-panel>
        <v-expansion-panel>
          <v-expansion-panel-header>待入院患者列表</v-expansion-panel-header>
          <v-expansion-panel-content>
            <v-data-table
              dense
              :headers="headers"
              :items="desserts"
              :search="search"
            ></v-data-table>
          </v-expansion-panel-content>
        </v-expansion-panel>
        <v-expansion-panel>
          <v-expansion-panel-header
            >出院患者列表(3个月)</v-expansion-panel-header
          >
          <v-expansion-panel-content>
            <v-card>
              <v-card-title>
                <v-text-field
                  v-model="search"
                  append-icon="search"
                  label="姓名或住院号"
                  single-line
                  hide-details @click:row="getpatient1($event)"
                ></v-text-field>
              </v-card-title>
              <v-data-table
                dense
                :headers="headers"
                :items="desserts"
                :search="search"
              ></v-data-table>
            </v-card>
          </v-expansion-panel-content>
        </v-expansion-panel>
      </v-expansion-panels>
    </v-navigation-drawer>

    <v-app-bar
      :clipped-left="$vuetify.breakpoint.lgAndUp"
      app
      color="blue darken-3"
      dark
    >
      <v-toolbar-title style="width: 300px" class="ml-0 pl-4">
        <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>
        <span class="hidden-sm-and-down">病房医生工作站</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-tooltip right>
        <template v-slot:activator="{ on }">
          <v-btn icon to="/about" v-on="on">
            <v-icon>thumb_up_alt</v-icon>
          </v-btn>
        </template>
        <span>帮助手册</span>
      </v-tooltip>
      <v-btn icon to="/">
        <v-icon>notifications</v-icon>
      </v-btn>
      <v-btn icon large @click="selectSource">
        <v-avatar size="32px" item>
          <v-img :src="require('../assets/logo.svg')" alt="苜蓿草科技"></v-img>
        </v-avatar>
      </v-btn>
    </v-app-bar>
    <!-- <v-container fluid fill-height>
      <v-layout justify-start>
        <v-img :src="require('../assets/main_bg.jpg')" />
      </v-layout>
    </v-container>-->
    <v-tooltip right>
      <template v-slot:activator="{ on }">
        <v-btn
          bottom
          color="pink"
          dark
          fab
          fixed
          right
          @click="clickMenu('logout')"
          v-on="on"
          ><v-icon>add</v-icon>
        </v-btn>
      </template>
      <span>退出登录</span>
    </v-tooltip>
  </div>
</template>

<script>
export default {
  props: {
    source: String
  },
  data: () => ({
    dialog: false,
    drawer: null,
    room: "",
    checkbox1: true,
    checkbox2: true,
    checkbox3: true,
    search: "",
    depts: [
      {text: "内一科一病区", value: "0101"},
      {text: "内一科二病区",value: "0102"}
    ],
    headers: [
      {
        text: "Dessert (100g serving)",
        align: "left",
        sortable: false,
        value: "name"
      },
      { text: "Calories", value: "calories" },
      { text: "Fat (g)", value: "fat" },
      { text: "Carbs (g)", value: "carbs" },
      { text: "Protein (g)", value: "protein" },
      { text: "Iron (%)", value: "iron" }
    ],
    desserts: [
      {
        name: "Frozen Yogurt",
        calories: 159,
        fat: 6.0,
        carbs: 24,
        protein: 4.0,
        iron: "1%"
      },
      {
        name: "Ice cream sandwich",
        calories: 237,
        fat: 9.0,
        carbs: 37,
        protein: 4.3,
        iron: "1%"
      },
      {
        name: "Eclair",
        calories: 262,
        fat: 16.0,
        carbs: 23,
        protein: 6.0,
        iron: "7%"
      },
      {
        name: "Cupcake",
        calories: 305,
        fat: 3.7,
        carbs: 67,
        protein: 4.3,
        iron: "8%"
      },
      {
        name: "Gingerbread",
        calories: 356,
        fat: 16.0,
        carbs: 49,
        protein: 3.9,
        iron: "16%"
      },
      {
        name: "Jelly bean",
        calories: 375,
        fat: 0.0,
        carbs: 94,
        protein: 0.0,
        iron: "0%"
      },
      {
        name: "Lollipop",
        calories: 392,
        fat: 0.2,
        carbs: 98,
        protein: 0,
        iron: "2%"
      },
      {
        name: "Honeycomb",
        calories: 408,
        fat: 3.2,
        carbs: 87,
        protein: 6.5,
        iron: "45%"
      },
      {
        name: "Donut",
        calories: 452,
        fat: 25.0,
        carbs: 51,
        protein: 4.9,
        iron: "22%"
      },
      {
        name: "KitKat",
        calories: 518,
        fat: 26.0,
        carbs: 65,
        protein: 7,
        iron: "6%"
      }
    ]
  }),
  methods: {
    
    getpatient(e){
      window.alert("click="+JSON.stringify(e))
      this.$router.push({ name: "patient", params: { patient: e } });

    },
    getpatient1(e){
      window.alert("click1="+JSON.stringify(e))
    },
    selectSource() {
      window.location.href = "http://www.cloveropen.com";
    }
  }
};
</script>
