
<template>
<div>
    <div id="main">

      <v-col cols="2" style="padding-right:0px">
        <div id="resultset-title">
          <span ><v-icon left>mdi-pencil-ruler</v-icon>Profit and Loss</span>
        </div>
        <!-- <div id="resultset-submenu">
          <v-navigation-drawer id="resultset-submenu-navlist" permanent floating>
            <v-list dense nav>
                <v-list-item v-for="(item, index) in resultsetmenu" :key="item.navname" @click="navtemplatelink(item.navname),resultsetmenuindex = index" link :class="resultsetmenuindex == index ? 'resultset-menu-nav-act': 'result-menu-nav'">
                  <v-list-item-icon>
                    <v-icon class="navicon">{{ item.icon }}</v-icon>
                  </v-list-item-icon>
                  <v-list-item-content style="text-transform: uppercase;">
                    <v-list-item-title class="resultset-menu-nav-title">{{ item.navname }}</v-list-item-title>
                  </v-list-item-content>
                  <v-list-item-icon v-if="index === resultsetmenuindex">
                    <v-icon right class="resultset-menu-nav-arrow">mdi-arrow-right-thick</v-icon>
                  </v-list-item-icon>
                </v-list-item>
            </v-list>
          </v-navigation-drawer>
        </div> -->

        <div id="resultset-component">
          <v-navigation-drawer permanent id="resultset-component-navlist" floating v-for="item in componentitem" :key="item.component">
            <v-list-item>
              <v-list-item-content>
                <v-list-item-title>
                  <v-icon left class="componenticon">{{item.icon}}</v-icon> {{item.component}}
                  <v-icon v-if="componentchecked.length >0 " class="component-download-icon" >mdi-download</v-icon>
                </v-list-item-title>
                <!-- <v-list-item-subtitle>
                  subtext
                </v-list-item-subtitle> -->
              </v-list-item-content>
            </v-list-item>
            <v-list dense>
              <v-list-item >
                <v-list-item-content id="component-content">
                  <!-- <v-list-item-title>{{ item.navname }}</v-list-item-title> -->
                  <v-checkbox v-for="componentfiles in item.title" :key="componentfiles.item" dense v-model="componentchecked" :label="`${componentfiles.item}`" color="success" :value="`${componentfiles.item}`" hide-details :ripple="false" class="component-checkbox"></v-checkbox>
                </v-list-item-content>
              </v-list-item>
            </v-list>
          </v-navigation-drawer>
        </div>
        <div></div>
      </v-col>
      <v-col cols="10">

        <v-stepper v-model="stepnow" flat style="background: transparent">
          <v-stepper-header  class="stepper-header" style="box-shadow:0 0 0;padding: 0 15px;">
            <template v-for="(item, index) in stepper" >
              <v-stepper-step  v-if="item" :key="item.key" :complete="stepnow > index+1" :step=index+1 editable color="#ADC9D2">
                {{item.title}}
              </v-stepper-step>
              <v-divider v-if="index < stepper.length-1" :key="index"></v-divider>
            </template>
          </v-stepper-header>

          <v-stepper-items class="stepper-items">
            <v-stepper-content step="1">
              <StepDetail :step="stepper[0]"/>
            </v-stepper-content>
            <v-stepper-content step="2">
                <StepDetail :step="stepper[1]"/>
            </v-stepper-content>
            <v-stepper-content step="3">
              <StepDetail :step="stepper[2]"/>
            </v-stepper-content>
            <v-stepper-content step="4">
              <StepDetail :step="stepper[3]"/>
            </v-stepper-content>
            <v-stepper-content step="5">
              <StepDetail :step="stepper[4]"/>
            </v-stepper-content>
            <div id="stepper-footer">
              <v-btn :ripple="false" plain class="stepper-saved">
                <v-icon style="margin-right:5px">mdi-content-save-outline</v-icon>SAVE
              </v-btn>
              <v-btn color="#D6E2E6" v-if="stepnow < stepper.length" @click="stepnow += 1" depressed class="stepper-btn" style="font-weight:600">Next</v-btn>
              <v-btn v-if="stepnow > 1" @click="stepnow -= 1" depressed style="background: #eee;margin-left: 5px;" class="stepper-btn">Prev</v-btn>
            </div>  
          </v-stepper-items>
        </v-stepper>

      </v-col>

    </div>

  </div>
</template>


<script>
import StepDetail from './StepDetail.vue';
  export default {
  components: { StepDetail },
    data: () => ({
      tabs: 1,
      resultsetmenu:[{navname:'Property',icon:'mdi-cog',link:'https://github.com/vuetifyjs/vuetify'},{navname:'Browse',icon:'mdi-table-large',link:'https://github.com/vuetifyjs/vuetify'}],
      componentitem:[
        {
          component:'Excel',
          icon:'mdi-file-excel',
          title:[
            {item:'Monthly Profit and Loss'},
            {item:'Profit and Loss by Division'},
            {item:'Yearly Profit and Loss'},
   
          ]
        }
      ],
      componentchecked:[],
      resultsetmenuindex:0,
      stepnow:1,
      stepper:[
        {"key":"property","title":"Property"},
        {"key":"sqlResult","title":"Sql Result"},
        {"key":"xlsEditor","title":"XLS Editor"},
        {"key":"finalResult","title":"Final Result"},
        {"key":"report","title":"Report"}
      ],
      resultsetbody:[{tabname:'Property',icon:'mdi-cog'},{tabname:'SQL',icon:'mdi-database'},{tabname:'Ask',icon:'mdi-table-key'}],
      navtemplate:'Property',
      JsonEditorHeaders: [
        {
          text: '',
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
        key: 'xvdate2',
        title: 'Date',
        datatype: 'Date',
        testvalue: '2021/06/01',
      },
      {
        btn: '',
        key: 'xvdate3',
        title: 'Date',
        datatype: 'Date',
        testvalue: '2021/12/01',
      },
      {
        btn: '',
        key: 'xvdate4',
        title: 'Date',
        datatype: 'Date',
        testvalue: '2022/01/01',
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
  /* color: #FF9800; */
  color: #000;
}
#resultset-title .v-icon{
  /* color: #FF9800; */
  color: #000;
}
/* #resultset-submenu{
  max-height:32%;
  min-height: fit-content;
  padding: 12px 12px 12px 0;
  background:green;
}
#resultset-submenu-navlist{
  border-radius: 12px;
  border: 0px;
  background: transparent;
}
.resultset-menu-nav-title{
  color: #757575;
  font-size: 16px!important;
  line-height: 20px;
}

.resultset-menu-nav:hover{
  background: #D6E2E6;
  border-radius: 12px!important;
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
} */

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
  box-shadow: 0px 3px 18px rgba(230,230,230,.8);
}
#resultset-component-navlist .v-list-item{
    /* padding-right: 8px; */
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
  /* padding: 0px; */
  overflow: auto;
  
}
#resultset-component-navlist label{
  color: #757575;
}
#resultset-component-navlist .v-input--checkbox{
  /* margin: 0; */
  padding: 0;
}
.component-checkbox{
  white-space: nowrap;
}
.component-checkbox .v-input--selection-controls__input{
  margin-right: 4px;
  position: sticky;
  left: 0;
  background: #fff;
}
.component-download-icon {
  float: right;
  color: #000!important;
}
#component-content{
  max-height: 31vh;
  padding: 3px 0px;
}
#component-content::-webkit-scrollbar {
    width: 0.4em;
    height: 0.4em;
}
#component-content::-webkit-scrollbar-track-piece:start {
    background: transparent;
}
#component-content::-webkit-scrollbar-thumb {
    background-color: #ddd;
    border-radius: var(--Menu-ListItem-ScrollBar-border-radius);
    background-clip: content-box;
}
#component-content::-webkit-scrollbar-track {
    background-color: #eee;
    border-radius: var(--STScrollBar-thumb-border);
    display: block;
    border: var(--STScrollBar-border);
}

.stepper-header{
  height: 60px!important;
}
.stepper-items{
  height: calc(100vh - 12px - 60px - 50px - 45px);
}
#stepper-footer{
  position: absolute;
  bottom: 5px;
}
.stepper-saved{
  margin:0 20px;
  /* background: #eaeaea; */
  border-radius: 4px;
}
.stepper-btn{
  padding: 0 50px!important;

}

</style>