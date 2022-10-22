
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
                <v-list-item v-for="(item, index) in resultsetmenu" :key="item.navname" @click="navtemplatelink(item.navname)" link class="result-menu-nav">
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
                  <v-icon v-if="componentchecked.length >0 " class="component-download-icon" >mdi-download</v-icon>
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
                  <v-checkbox dense v-model="componentchecked" :label="`${item.navname}`" color="success" :value="`${item.navname}`" hide-details :ripple="false"></v-checkbox>
                </v-list-item-content>
              </v-list-item>
            </v-list>
          </v-navigation-drawer>
        </div>
        <div></div>
      </v-col>
      <v-col cols="10">
        <template v-if="navtemplate == 'Property'">
          <v-tabs v-model="tabs" class="resultset-tabs" hide-slider background-color="transparent">
            <!-- <v-hover v-slot="{ hover }"> -->
            <v-tab v-for="item in resultsetbody" :key="item.tabname" class="resultset-tab"  active-class="resultset-tab-act" :ripple="false">
              <v-icon>{{ item.icon }}</v-icon>{{item.tabname}}
            </v-tab>
            <v-btn icon :ripple="false" plain style="margin:0 20px">
              <v-icon>mdi-content-save-outline</v-icon>
            </v-btn>
            <!-- </v-hover> -->
          </v-tabs>
          
          <v-tabs-items v-model="tabs" style="background: transparent;padding: 0 5px 20px 5px;">
            
            <v-tab-item>
              <v-card class="tab-property-card">
                <v-list-item class="tab-property-card-content">
                  <v-list-item-content>
                      
                  </v-list-item-content>
                </v-list-item>
              </v-card>
            </v-tab-item>

            <v-tab-item>
              <v-card class="tab-card">
                <v-list-item class="tab-card-content">
                  <v-list-item-content>
                      <div class="tab-card-content-title"><v-icon left>mdi-menu</v-icon>SQL</div>
                      <v-divider></v-divider>
                      <textarea class="tab-card-content-text">123</textarea>
                  </v-list-item-content>
                </v-list-item>
              </v-card>
              <v-card class="tab-card tab-card-JsonEditor">
                <v-list-item class="tab-card-content">
                  <v-list-item-content>
                      <div class="tab-card-content-title"><v-icon left>mdi-menu</v-icon>Ask</div>
                      <v-divider></v-divider>
                      <v-data-table :headers="JsonEditorHeaders" :items="JsonEditorItem" item-key="name" :items-per-page="5">
                        <!-- <template v-slot:item.calories="{ item }">
                          <v-icon :color="getColor(item.calories)" dark>
                            {{ item.calories }}
                          </v-icon>
                        </template> -->
                      </v-data-table>
                  </v-list-item-content>
                </v-list-item>
              </v-card>
            </v-tab-item>
          
            <v-tab-item>
            </v-tab-item>

            <v-tab-item>
            </v-tab-item>
          </v-tabs-items>
        </template>

        <template v-if="navtemplate == 'Browse'">
        </template>
      </v-col>

    </div>

  </div>
</template>


<script>
  export default {
    data: () => ({
      tabs: 1,
      resultsetmenu:[{navname:'Property',icon:'mdi-cog',link:'https://github.com/vuetifyjs/vuetify'},{navname:'Browse',icon:'mdi-table-large',link:'https://github.com/vuetifyjs/vuetify'}],
      componentchecked:[],
      resultsetmenuindex:0,
      resultsetbody:[{tabname:'Property',icon:'mdi-cog'},{tabname:'SQL',icon:'mdi-database'},{tabname:'DATAMODEL',icon:'mdi-database'}],
      navtemplate:'Property',
      JsonEditorHeaders: [
        {
          text: 'Dessert (100g serving)',
          align: 'start',
          value: 'btn',
        },
        { text: 'Key', value: 'key' },
        { text: 'Title', value: 'title' },
        { text: 'Data Type', value: 'datatype' },
        { text: 'Test Value', value: 'testvalue' },
    ],
    JsonEditorItem: [
      {
        btn: '',
        key: 'xvdate1',
        title: 'Date',
        datatype: 'Date',
        testvalue: '2021/01/01',
      },
      {
        btn: '',
        key: 'xvdate1',
        title: 'Date',
        datatype: 'Date',
        testvalue: '2021/01/01',
      },
      {
        btn: '',
        key: 'xvdate1',
        title: 'Date',
        datatype: 'Date',
        testvalue: '2021/01/01',
      },
      {
        btn: '',
        key: 'xvdate1',
        title: 'Date',
        datatype: 'Date',
        testvalue: '2021/01/01',
      },
      {
        btn: '',
        key: 'xvdate1',
        title: 'Date',
        datatype: 'Date',
        testvalue: '2021/01/01',
      },
      {
        btn: '',
        key: 'xvdate1',
        title: 'Date',
        datatype: 'Date',
        testvalue: '2021/01/01',
      },
      {
        btn: '',
        key: 'xvdate1',
        title: 'Date',
        datatype: 'Date',
        testvalue: '2021/01/01',
      },
    ],
    }),
    methods:{
      navtemplatelink(temp){
        this.navtemplate = temp;
      }
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
.component-download-icon {
  float: right;
  color: #000!important;
}



.resultset-tabs .v-slide-group__content {
    justify-content: end;
    align-items: center;
}
.resultset-tab {
    /* color: #000!important; */
    background: transparent;
    margin: 0 0px!important;
    padding: 12px 15px;
    z-index: 1;
    font-size: 14px;
    position: relative;
    display: flex;
    align-items: center;
    font-weight: medium;
}
.resultset-tab:before {
    content: "";
    position: absolute;
    right: 0;
    bottom: 0;
    left: 0;
    z-index: -1;
    background: #ebebeb!important;
    border-radius: 1.5em 1.5em 0 0;
    transform: scale(1.08) perspective(1.8em) rotateX(4deg);
    transform-origin: bottom;
    transition: .2scubic-bezier(.4,0,.6,1);
    opacity: 1;
    height: 55px;
}
.resultset-tab-act{
  z-index: 2;
  color: #000!important;
}
.resultset-tab-act:before{
  content: "";
  position: absolute;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: -1;
  background: #fff!important;
  z-index: -1;
  opacity:1!important;
}
.theme--light.v-tabs .v-tab:hover::before {
    /* opacity: 0.6;
    background: #fff!important; */
}
.resultset-tabs .resultset-tab:hover::before {
    opacity: 0.6!important;
    background: #fff!important;
}

.tab-property-card{
  font-size: 16px;
  min-height: 20vh;
  box-shadow: 0px 3px 18px rgba(68,67,67,.05)!important;
  background: #fff!important;
  border-radius: 12px!important;
}
.tab-property-card-content{
  padding: 0;
}
.tab-card{
  font-size: 16px;
  min-height: 20vh;
  box-shadow: 0px 3px 18px rgba(68,67,67,.05)!important;
  background: #fff!important;
  border-radius: 12px!important;
  margin-bottom: 15px;
}
.tab-card-JsonEditor{
  min-height: fit-content;
}
.tab-card-content{
  padding: 0;
}
.tab-property-card-content .v-icon{
  color:#A0B2B6;
}
.tab-card-content-title{
  font-size: 20px;
  padding: 5px 20px;
  margin-bottom: 0;
  font-weight: 600;
  display: flex;
  align-items: center;
}
.tab-card-content-text{
  padding: 8px;
  outline: none;
  min-height: calc(20vh - 40px);
}
.tab-card .v-list-item{
  min-height: auto;
}
.tab-card .v-list-item__content{
  padding: 0px!important;
  margin: 0;
}
.tab-card .v-list-item__content > *:not(:last-child){
  margin: 0;
}

</style>