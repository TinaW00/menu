
<template>
<div>
    <div id="main">

      <v-col cols="2" style="padding-right:20px">
        <div id="resultset-title">
          <span ><v-icon left>mdi-pencil-ruler</v-icon>Profit and Loss</span>
        </div>
        <div id="resultset-submenu">
          <v-navigation-drawer id="resultset-submenu-navlist" permanent floating>
            <v-list dense nav>
              <v-list-item-group v-model="resultsetmenuindex" class="resultset-menu-nav-group" active-class="resultset-menu-nav-act">
                <v-list-item v-for="(item, index) in resultsetmenu" :key="item.navname" link class="result-menu-nav">
                  <v-list-item-icon>
                    <v-icon class="navicon">{{ item.icon }}</v-icon>
                  </v-list-item-icon>
                  <v-list-item-content style="text-transform: uppercase;">
                    <v-list-item-title>{{ item.navname }}</v-list-item-title>
                  </v-list-item-content>
                  <v-list-item-icon v-if="index === resultsetmenuindex">
                    <v-icon right class="resultset-menu-nav-arrow">mdi-arrow-right-thick</v-icon>
                  </v-list-item-icon>
                </v-list-item>
                
              </v-list-item-group>
            </v-list>
          </v-navigation-drawer>

        </div>
        <div id="resultset-component">
          <v-navigation-drawer permanent id="resultset-component-navlist" floating>
            <v-list-item>
              <v-list-item-content>
                <v-list-item-title>
                  <v-icon left class="componenticon">mdi-file-excel</v-icon> Excel
                </v-list-item-title>
                <!-- <v-list-item-subtitle>
                  subtext
                </v-list-item-subtitle> -->
              </v-list-item-content>
            </v-list-item>
            <v-list dense>
              <v-list-item v-for="item in resultsetmenu" :key="item.navname">
                <v-list-item-content>
                  <!-- <v-list-item-title>{{ item.navname }}</v-list-item-title> -->
                  <v-checkbox dense v-model="resultsetcomponent" :label="`${item.navname}`" color="success" :value="`${item.navname}`" hide-details :ripple="false"></v-checkbox>
                </v-list-item-content>
              </v-list-item>
            </v-list>
          </v-navigation-drawer>
        </div>
        <div></div>
      </v-col>
      <v-col cols="10">
        <template>
          <v-tabs v-model="tabs" class="resultset-tabs" hide-slider background-color="transparent">
              <v-tab v-for="item in resultsetbody" :key="item.tabname" class="resultset-tab"  active-class="resultset-tab-act">
                <v-icon>{{ item.icon }}</v-icon>{{item.tabname}}
              </v-tab>
            </v-tabs>
            
            <v-tabs-items v-model="tabs" style="background: transparent;">
              <v-tab-item>
              </v-tab-item>

              <v-tab-item>
              </v-tab-item>

              <v-tab-item>
              </v-tab-item>

              <v-tab-item>
              </v-tab-item>
            </v-tabs-items>
        </template>
      </v-col>

    </div>

  </div>
</template>


<script>
  export default {
    data: () => ({
      resultsetmenu:[{navname:'Property',icon:'mdi-cog'},{navname:'Browse',icon:'mdi-table-large'}],
      resultsetcomponent:[],
      resultsetmenuindex:0,
      resultsetbody:[{tabname:'Property',icon:'mdi-cog'},{tabname:'SQL',icon:'mdi-database'},{tabname:'DATAMODEL',icon:'mdi-database'}],
    }),
    methods:{
      
    }
  }
</script>

<style>
:root{
  --Menu-bg : #fff;
  --Menu-Tabs-border: 4px solid;
  --Menu-Tabs-border-color : #A0B2B6;
  --Menu-Tab-width-height : 40px;
  --Menu-Tab-border-radius : 12px;
  --Menu-Tab-bg : #F0F4F5;
  --Menu-Tab-color : #555353;
  --Menu-Tab-font-size: 30px;
  --Menu-Tab-Act-color: #555353;
  --Menu-Tab-Act-font-size :28px;
  --Menu-ListItem-bg : #f9f9f9;
  --Menu-ListItem-Title-color : #A0B2B6;
  --Menu-ListItem-GroupHeader-color : #757575;
  --Menu-ListItem-GroupHeader-HoverAct-color : #A0B2B6;
  --Menu-ListItem-GroupContent-icon-color : #A0B2B6;
  --Menu-ListItem-GroupContent-color : #888;
  --Menu-ListItem-ScrollBar-width-height : 0.4em;
  --Menu-ListItem-ScrollBar-border-radius : 50px;
  --Menu-ListItem-ScrollBar-color : #ccc;
  --Menu-ListItem-ScrollBar-bg : #eee;
  --Menu-Dashboard-Selected-color : #A0B2B6;

  --System-Body-bg :#F5f5f5;
  --Menu-Dashboard-icon-color :#A0B2B6;
  --System-Top-select--comma-color :#A0B2B6;
}
*{
  font-family: 'inter';
}
.v-main__wrap{
  background:#f5f5f5;
}
#main{
  position: relative;
  height: calc(100vh - 49px);
  display: flex;
  padding-left: 70px;
}
#resultset-title{
  height:8%;
  /* background:blue; */
  display: flex;
  align-items: center;
  padding: 12px;
  font-size:20px;
  font-weight:600;
  color: #FF9800;
}
#resultset-title .v-icon{
  color: #FF9800;
}
#resultset-submenu{
  max-height:32%;
  min-height: fit-content;
  padding: 12px 12px 12px 0;
  /* background:green; */
}
#resultset-submenu-navlist{
  border-radius: 12px;
  border: 0px;
  background: transparent;
}
.resultset-menu-nav-group .v-list-item__title{
  color: #757575;
  font-size: 16px!important;
  line-height: 20px;
}
.resultset-menu-nav-group{
  color: #757575;
}
.resultset-menu-nav-group{
  color: #757575;
}
.resultset-menu-nav:hover{
  background: #D6E2E6;
}
.resultset-menu-nav-arrow{
  font-size: 20px!important;
  color: #A0B2B6!important; 
}
.resultset-menu-nav .v-list--nav .v-list-item, .v-list--nav .v-list-item:before{
  border-radius: 12px!important;
}
.resultset-menu-nav-act{
  background: #D6E2E6;
  border-radius: 12px!important;
}
.resultset-menu-nav-act .v-list-item__title{
  color: #000;
  font-weight: 600!important;
}
.resultset-menu-nav-act .navicon{
  color: #000!important;
}

#resultset-component{
  max-height:60%;
  min-height: fit-content;
  padding: 12px 12px 12px 0;
  /* background:red; */
}
#resultset-component-navlist{
  border-radius: 12px;
  border: 0px;
  background: #fff;
}
#resultset-component-navlist .v-list-item__title{
  color: #65C468;
  font-size: 18px;
  font-weight: 600;
}
#resultset-component-navlist .componenticon{
  color: #65C468;
}
#resultset-component-navlist .v-list-item__content{
  padding: 0px;
  
}
#resultset-component-navlist label{
  color: #757575;
}
#resultset-component-navlist .v-input--checkbox{
  margin: 0;
  padding: 0;
}

.resultset-tab {
    /* color: #000!important; */
    background: transparent!important;
    margin: 0 0px!important;
    padding: 12px 15px;
    z-index: 1;
    font-size: 14px;
    position: relative;
    display: flex;
    align-items: center;
}
.resultset-tab::before {
    content: "";
    position: absolute;
    right: 0;
    bottom: 0;
    left: 0;
    z-index: -1;
    background: #EBEBEB!important;
    border-radius: 1.5em 1.5em 0 0;
    transform: scale(1.08) perspective(1.8em) rotateX(4deg);
    transform-origin: bottom;
    transition: .2scubic-bezier(.4,0,.6,1);
    opacity: 1;
    height: 55px;
}

.resultset-tab-act::before{
  content: "";
  position: absolute;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: -1;
  background: #000!important;
  z-index: 1;
}
.resultset-tab-act:before{
  opacity:1!important;
  z-index: -1;
}

</style>