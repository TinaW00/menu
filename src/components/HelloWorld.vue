
<template>
<div>
 <v-toolbar flat dense style="z-index: 99;">                     <!-- Tool bar  -->
        <v-btn icon  class="menu-btn" @click.stop="drawer = !drawer, MenuTabIndex = 1" :ripple="false" v-ripple="false"><v-icon  large>mdi-text-short</v-icon></v-btn>          <!-- Home button  -->
        
        <v-col cols="auto">        
          <div id="select">
            <v-select class="selectinput dashboard" :items="dashboard" v-model="develop" item-text="text" flat hide-details prepend-icon="mdi-collage" append-icon="" color="#A0B2B6" dense :menu-props="{ bottom: true, offsetY: true, maxHeight: 'auto' }">
            </v-select>
          </div>
        </v-col>
        <v-divider vertical></v-divider>
        <v-spacer></v-spacer>

        <v-img src="http://210.3.65.166/pgsfm3k/template/swivel2.png" max-height="60" max-width="120" contain></v-img>        <!-- LOGO  -->
        <v-spacer></v-spacer>

    <v-row style="display:flex;justify-content: space-around;flex-wrap: nowrap;" id="top-select">
        <v-col cols="auto">      <!-- tenants  -->
          <div id="select" class="tenantstitleAct">
            <v-select class="selectinput" :items="tenants" item-text="tenant" item-value="tenant" flat hide-details label="Tenant" append-icon="mdi-chevron-down" color="#000" dense :menu-props="{ bottom: true, offsetY: true, maxHeight: 'auto' }">
               <template v-slot:prepend-item></template>
                    <template v-slot:selection="data">
                        <v-list-item-avatar  style="height:24px;width:24px;min-width: 24px;margin:0px;">
                            <v-img src="https://picsum.photos/id/11/500/300"></v-img>
                            <span ></span>
                        </v-list-item-avatar>
                        <v-list-item-action-text class="pl-2">
                            <v-list-item-title v-html="data.item.tenant"></v-list-item-title>
                        </v-list-item-action-text>
                    </template>
                    <template v-slot:item="data">
                        <v-list-item-avatar  style="height:35px;width:35px;min-width: 35px;margin:5px 10px 5px 0px;">
                            <v-img  src="https://picsum.photos/id/11/500/300"></v-img>
                        </v-list-item-avatar>
                        <v-list-item-action-text>
                            <v-list-item-title v-html="data.item.tenant" ></v-list-item-title>
                        </v-list-item-action-text>
                    </template>

            </v-select>
          </div>
        </v-col>
        <v-col cols="auto">         <!-- User -->
          <div id="select">
            <v-select :items="options" flat hide-details prefix="User" append-icon="mdi-chevron-down" color="#000" dense :menu-props="{ bottom: true, offsetY: true, maxHeight: 'auto' }">
            </v-select>
          </div>
        </v-col>
        <v-col cols="auto" >        <!-- Menu -->
          <div id="select">
            <v-select class="selectinput" :items="options" flat hide-details hide-selected append-icon="mdi-chevron-down" label="Menu" color="#000" dense :menu-props="{ bottom: true, offsetY: true, maxHeight: 'auto' }">
            </v-select>
          </div>
        </v-col>
        <v-col cols="auto" >        <!-- Role -->
          <div id="select">
            <v-select class="selectinput" :items="options" item-color="grey darken-1" small-chips deletable-chips flat hide-details prefix="Role" append-icon="mdi-chevron-down" color="#000" dense :menu-props="{ bottom: true, offsetY: true, maxHeight: 'auto' }">
              <template #selection="{ item }">
                <v-chip outlined color="#2660A4" style="max-height:27px">{{item.text}}</v-chip>
              </template>
            </v-select>
          </div>
        </v-col>
    </v-row>
        <v-spacer></v-spacer>

       <v-row>
        <v-col class="searchbar">         <!-- search bar   -->
          <v-text-field solo flat dense hide-details label="Search" append-icon="mdi-magnify" background-color="#f1f1f1" ></v-text-field>
        </v-col>
        </v-row>
        <v-spacer></v-spacer>
        
        <v-btn icon>
          <v-icon>mdi-history</v-icon>
        </v-btn>
        <v-btn icon>
          <v-icon>mdi-cog-outline</v-icon>
        </v-btn>
        <v-btn icon>
          <v-icon>mdi-palette-outline</v-icon>
        </v-btn>
        <v-menu offset-y open-on-click close-on-content-click >           <!-- Translate button -->
          <template v-slot:activator="{ on }">
            <v-btn color="grey darken-1" text v-on="on">
                <v-icon>mdi-translate</v-icon><v-icon right>mdi-chevron-down</v-icon>
            </v-btn>
          </template>
          <v-list dense nav>
            <v-list-item v-for="(item, index) in languages" :key="index" :href="item.link" link>
              <v-list-item-title>
                <v-icon>{{item.icon}}</v-icon> {{ item.title }}</v-list-item-title>
            </v-list-item>
          </v-list>
        </v-menu>
        <v-spacer></v-spacer>
        
     <!--   Theme button
        <v-tooltip left>
          <template v-slot:activator="{ on, attrs }">
            <v-menu offset-y open-on-click close-on-content-click >  
              <template v-slot:activator="{ on }">
                <v-btn color="grey darken-1" text v-on="on">
                    <v-icon left>mdi-circle-half-full</v-icon>Theme
                </v-btn>
              </template>
              <v-list dense nav>
                <v-list-item v-for="(item, index) in theme" :key="index" :href="item.link" link v-bind="attrs" v-on="on">
                  <v-list-item-title>
                    <v-icon>{{item.icon}}</v-icon> {{ item.title }}</v-list-item-title>
                </v-list-item>
              </v-list>
            </v-menu>
          </template>
          <span>{{item}}</span>
        </v-tooltip>
    -->
          <template>
            <v-menu offset-y open-on-click close-on-content-click >
              <template v-slot:activator="{ on }">
                <v-btn color="grey darken-1" text v-on="on">
                    <v-icon left>mdi-circle-half-full</v-icon>Theme
                </v-btn>
              </template>
                  <v-list dense nav>
                    <v-list-item v-for="(item, index) in theme" :key="index" :href="item.link" link >
                       <v-tooltip left color="#fff" nudge-top="5" nudge-left="12">
                          <template v-slot:activator="{ on, attrs }"> 
                             <v-list-item-title v-bind="attrs" v-on="on"><v-icon>{{item.icon}}</v-icon> {{ item.title }}</v-list-item-title>
                          </template>
                          <span><v-img :src="require(`../assets/${item.img}`)"  width="350" aspect-ratio="1.7" contain></v-img></span>
                        </v-tooltip>
                   </v-list-item>
                 </v-list>
            </v-menu>
          </template>

    </v-toolbar>
    <v-divider></v-divider>


    <v-navigation-drawer absolute style="width:min-content;" v-model="drawer" :mini-variant.sync="mini" class="nav-drawer">
     
        <v-list-item> 
           <v-icon></v-icon>
            <v-list-item-content >
              <v-list-item-title></v-list-item-title>
            </v-list-item-content>
        </v-list-item>
        <v-divider></v-divider>


        <v-tabs vertical v-model="MenuTabIndex" hide-slider class="menu-tabs"  active-class="menu-act-tabs">
          <v-tab style="display:none"></v-tab>
          <v-tab v-for="(item, index) in block" :key="index" @click="tabcount(index)" :ripple="false" class="menu-tab" active-class="menu-act-tab" :style="{ '--lighten': (lighten-index*10)+ '%' }">
            <v-icon>{{item.icon}}</v-icon>
          </v-tab>
         
         <v-tab-item></v-tab-item>
          <v-tab-item v-for="item in block" :key="item.module" class="menu-tab-item" transition=" ">
            <v-list dense nav shaped>
              <v-list-item>
                <header class="menu-tab-item-header">
                  {{ item.module }}
                  <v-icon @click.stop="mini = !mini" @click="deselect, drawer = !drawer" class="menu-tab-item-header-close">mdi-close-circle-outline</v-icon>
                </header>
              </v-list-item>
              <div id="menu-tab-item-scrollbar">
                <v-list-group sub-group v-for="(subitem, index) in item.submodule" :key="index" @click="changeicon(index)" :append-icon="expandtab.includes((index + tabseries)) ? 'mdi-minus' : 'mdi-plus'" :prepend-icon="expandtab.includes((index + tabseries)) ? 'mdi-minus' : 'mdi-plus'" no-action :color="`var(--Menu-ListItem-GroupHeader-HoverAct-color)`" class="menu-tab-item-list-group" style="padding-left:0px!important;">
                  <template v-slot:activator>
                    <v-list-item-content>
                      <v-list-item-title>{{ subitem.title }}</v-list-item-title>
                    </v-list-item-content>
                  </template>

                  <v-list-item v-for="child in subitem.program" :key="child.title" style="padding-left:35px;" class="menu-tab-item-list-item" link>
                    <v-list-item-content>
                      <v-list-item-title><v-icon left small>{{child.icon}}</v-icon>{{ child.title }}</v-list-item-title>
                    </v-list-item-content>
                  </v-list-item>
                </v-list-group>
               </div>
            </v-list>
          </v-tab-item>
        </v-tabs>
      </v-navigation-drawer>
      <!-- <ResultSetUI/> -->
      <MenuJson/>
  </div>
  
</template>
<!--
<template>
  <div>
    <template>
      <div v-if="option == 0" class="d-inline-flex flex-wrap" style="width:100%;height: 400px;margin:0 auto;box-sizing: border-box;background:#555;">
        <v-card outlined v-if="tables.length" v-for="(table,index) in tables" :key="table"  :style="{'flex-basis':(tables.length % tablecount(tables.length)=== 0) ? mainwidth(tablecount(tables.length)) : index > stay(tables.length, tablecount(tables.length))-1 ? subwidth(tables.length,tablecount(tables.length)) : mainwidth(tablecount(tables.length)), 'margin':'0.2%'}">{{table.text}}</v-card>
      </div>
    </template>
    <template>
      <div v-if="option == 1" class="d-inline-flex flex-wrap" style="width:100%;height: 400px;margin:0 auto;box-sizing: border-box;background:#555;">
        <v-card outlined v-if="tables.length" v-for="(table,index) in tables" :key="table"  :style="{'flex-basis':(tables.length % 3 === 0) && (index+1) % 3 === 0 && index > tables.length-2? mainwidth(1) :(tables.length % 3 === 0) && (index+1) % 3 > 0 ? mainwidth(2) : (tables.length % 3 === 1) && ((index+1) % 3) === 1 && index > tables.length-2 ? mainwidth(1) :  ((index+1) % 3) > 0 ? mainwidth(2) : mainwidth(1) , 'margin':'0.2%'}">{{table.text}}</v-card>
      </div>
    </template>
    <template>
      <div v-if="option == 2" class="d-inline-flex flex-wrap" style="width:100%;height: 400px;margin:0 auto;box-sizing: border-box;background:#555;">
        <v-card outlined v-if="tables.length" v-for="(table,index) in tables" :key="table"  :style="{'flex-basis':index === 0 || (index % 4) === 0 ? mainwidth(1) : index > (Math.floor(tables.length/(4.1))*4)-1 ? mainwidth(tables.length-((Math.floor(tables.length/(4.1)))*4)-1) : mainwidth(3), 'margin':'0.2%'}">{{table.text}}</v-card>
      </div>
    </template>
    <v-btn outlined color="blue" @click="option0()" class="mt-5 ml-2" small>option 0</v-btn>
    <v-btn outlined color="green" @click="option1()" class="mt-5 ml-2" small>option 1</v-btn>
    <v-btn outlined color="orange" @click="option2()" class="mt-5 ml-2" small>option 2</v-btn>
    <v-btn outlined color="black" @click="plus(tables.length+1)" class="mt-5 ml-6" small>plus</v-btn>
    <v-btn outlined color="black" @click="minus()" class="mt-5 ml-2" small>minus</v-btn>
  </div>
</template>
<template>
  <div>
      <v-expansion-panels accordion active-class="act-badg-num">
        <v-expansion-panel v-for="(item,i) in 5" :key="i">
          <v-expansion-panel-header><v-badge inline content="6" class="badg-num" color="">Item</v-badge></v-expansion-panel-header>
          <v-expansion-panel-content></v-expansion-panel-content>
        </v-expansion-panel>
      </v-expansion-panels>

  </div>

 
</template>
-->

<script>
// import ResultSetUI from './ResultSetUI';
import MenuJson from './MenuJson';
import pmenu from "./menu.json";
  export default {
    components: {
    // ResultSetUI,
    MenuJson
  },
    data: () => ({
      lighten: 0,
      expand: false,
      expandone: -1,
      expandtab:[],
      // MenuTabIndex: 1,
      MenuTabIndex: 0,
      tabseries: 0,
      develop:{text:'Develop',value:'Develop'},
      dashboard:[
        {text:'Develop',value:'Develop'},
        {text:'Live',value:'Live'},
      ],
      block:pmenu,
      search_type:[
        {icon:'',title:'All',link:''},
        {icon:'',title:'Food',link:''},
        {icon:'',title:'Event',link:''},
        {icon:'',title:'Band',link:''},
        {icon:'',title:'Movie',link:''},
      ],
      // drawer: false,
      drawer: true,
      mini: true,
      miniopen: false,

      tables:[
        {text:'Table1'},
      ],
      theme:[
        {icon:'',title:'Default',link:'',img:'default.png'},
        {icon:'',title:'Blue',link:'',img:'blue.png'},
        {icon:'',title:'White',link:'',img:'white.png'},
        {icon:'',title:'Image',link:'',img:'image.png'},
        {icon:'',title:'Vintage',link:'',img:'vintage.png'},
        {icon:'',title:'Yellow',link:'',img:'yellow.png'},
        {icon:'',title:'Red',link:'',img:'red.png'},
        {icon:'',title:'Green',link:'',img:'green.png'},
        {icon:'',title:'Dark',link:'',img:'dark.png'}
      ],
      languages:[
        {icon:'',title:'English',link:''},
        {icon:'',title:'繁體中文',link:''},
        {icon:'',title:'日本語',link:''},
        {icon:'',title:'한국어',link:''},
      ],
      options: [
        {header:'header'},
        {text:'All',value:'All'},
        {text:'Active',value:'Active'},
        {text:'Not Print',value:'Not Print'},
        {text:'Incompolete',value:'Incompolete'},
        {header:'header',value:'header'},
        {text:'Header',value:'Header'},
        {text:'Ready to Post',value:'Ready to Post'},
        {text:'Posted',value:'Posted'},
        {text:'Missing Tax Invoice',value:'Missing Tax Invoice'}
        ],
      tenants:[
        {tenant:"ABC"},
        {tenant:"DEF"}
        ],
        option:0,
    }),
    methods:{
      deselect(){
        this.MenuTabIndex = -1;
      },
      changeicon(i){
        this.expandone = i+ this.tabseries;
        this.expand = !this.expand;
        if(this.expandtab.includes(this.expandone)){
          var index = this.expandtab.indexOf(this.expandone);
          if (index !== -1) {
            this.expandtab.splice(index, 1);
          }
        }else{
          this.expandtab.push(this.expandone)
        }
      },
      tabcount(tabnumber){
        this.tabseries = tabnumber * 100
      },
      tablecount(x){
        if((x / 1) == 1){
          return 1
        }
        else if((x % 10) == 0){
          return 2
        }
        else if((x % 5) == 0){
          return 3
        }
        else if((x % 7) == 0){
          return 3
        }
        else if((x % 3) == 0){
          return 3
        }
        else if((x % 2) == 0){
          return 2
        }
      },
      stay(l, w){
        return (w*Math.floor(l / w))
      },
      remain(l, w){
        return (l - (w*Math.floor(l / w)))
      },
      mainwidth(w){
        return ((100-(0.4* w)) / (w) +'%')
      },
      subwidth(l, w){
        return ((100-(0.4* (this.tablecount(l - (w*Math.floor(l / w)))))) / (this.tablecount(l - (w*Math.floor(l / w)))) +'%')
      },
      row(l, w){
        return (Math.floor(l / w))
      },
      setheight(tablerow){
          var h = (100-(0.4* tablerow)) / tablerow;
          return h+'%'
      },
      plus(n){
        var data = {text:'Table'+n};
        this.tables.push(data)
      },
      minus(){
        this.tables.pop()
      },
      option0(){
        this.option = 0
        return this.option
      },
      option1(){
        this.option = 1
        return this.option
      },
      option2(){
        this.option = 2
        return this.option
      },
      gethsl(){
        let colorcode = getComputedStyle(document.documentElement).getPropertyValue('--hsl');
        console.log("the color it received: ",colorcode);
        const hsloriginal = colorcode;
        const getlighten = /\d+/g;
        const hslarr = hsloriginal.match(getlighten);
        console.log("the lighten value of the color: ",hslarr[2]);
        this.lighten = parseInt(hslarr[2], 10);
        
      }
    },
    mounted(){
      this.gethsl()
    }
  }
</script>
<style lang="scss">
:root{
  --hsl : hsl(195,29%,75%);
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
.menu-btn:before{
  transform: scale(0.8);
  border-radius: 8px;
}
.nav-drawer{
  background: var(--Menu-bg)!important;
  padding-left: 5px;
  /* min-width: 61px!important; */
  min-width: 52px!important;
}
.menu-tabs{
	z-index:99;
	max-width:100%;
}
.menu-act-tabs{
  border: var(--Menu-Tabs-border);
  border-color: var(--Menu-Tabs-border-color);
  z-index:10;
  transition: .18s;
}
.menu-tab{
	min-width: var(--Menu-Tab-width-height);
	max-width: var(--Menu-Tab-width-height);
  max-height: var(--Menu-Tab-width-height);
	padding: 0px 0px;
  border-radius: var(--Menu-Tab-border-radius);
  background: hsl(195,29%,var(--lighten));
  margin: 5px 0;
}
.menu-act-tab{
  background: #ADC9D2;
}
.menu-tab > .v-icon{
  font-size: var(--Menu-Tab-font-size);
  color: var(--Menu-Tab-color);
}
.menu-act-tabs > .v-icon{
  font-size: var(--Menu-Tab-Act-font-size);
  color: var(--Menu-Tab-Act-color);
}

.menu-tab:before{
  opacity:0!important;
}
.menu-tab-item-list-group .v-list-group__header.v-list-item--active:not(:hover):not(:focus):before {
    opacity: 0.12;
}
.menu-tab-item-list-group .v-list-group__header.v-list-item{
  transition: color .1s;
}
.menu-tab-item-list-group .v-list-group__header.v-list-item:not(.v-list-item--active):not(.v-list-item--disabled){
  color: var(--Menu-ListItem-GroupHeader-color)!important;
}
.menu-tab-item-list-group .v-list-group__header.v-list-item:not(.v-list-item--active):not(.v-list-item--disabled) .v-icon{
  color: var(--Menu-ListItem-GroupHeader-color)!important;
}
.menu-tab-item-list-group .v-icon{
  font-size: 16px;
}
.menu-tab-item-list-group .v-list-group__header.v-list-item:hover{
  color:var(--Menu-ListItem-GroupHeader-HoverAct-color)!important;
}
.menu-tab-item-list-group .v-list-group__header.v-list-item:hover .v-icon{
  color:var(--Menu-ListItem-GroupHeader-HoverAct-color)!important;
}
.menu-tab-item-list-item .v-list-item__content{
  color:var(--Menu-ListItem-GroupContent-color);
}
.menu-tab-item-list-item .v-icon{
  color:var(--Menu-ListItem-GroupContent-icon-color);
}


.menu-tab-item{
  background: var(--Menu-ListItem-bg);
  padding: 0px;
  min-height: calc( 100vh - 49px );
  width: -webkit-fill-available;
  width: -moz-fill-available;
  width: -moz-available;
  width: fill-available;
  margin-left: 5px;
  position: relative;
}
.menu-tab-item::before{
  content: '';
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  opacity: 0.2;
  background-image: url('https://images.pexels.com/photos/1366919/pexels-photo-1366919.jpeg')!important;
  background-repeat: no-repeat;
  background-size: cover;
  
}
.menu-tab-item-header{
	font-weight:600;
	color: var(--Menu-ListItem-Title-color);
	display:flex;
	justify-content: space-between;
	width: 100%;
}
.menu-tab-item-header-close{
  color: var(--Menu-ListItem-Title-color)!important;
  font-weight:400;
}
#menu-tab-item-scrollbar{
  height:calc(100vh - 49px - 60px);
  overflow: hidden;
  padding-right: 15px;
}
.menu-tab-item:hover #menu-tab-item-scrollbar{
  overflow: overlay;
}
#menu-tab-item-scrollbar::-webkit-scrollbar {
    width: var(--Menu-ListItem-ScrollBar-width-height);
    height: var(--Menu-ListItem-ScrollBar-width-height);
    border-radius: var(--Menu-ListItem-ScrollBar-border-radius);
}
#menu-tab-item-scrollbar::-webkit-scrollbar-track-piece:start {
    background: transparent;
}
#menu-tab-item-scrollbar::-webkit-scrollbar-thumb {
    background-color: var(--Menu-ListItem-ScrollBar-color);
    border-radius: var(--Menu-ListItem-ScrollBar-border-radius);
    background-clip: content-box;
}
#menu-tab-item-scrollbar::-webkit-scrollbar-track {
    background-color: var(--Menu-ListItem-ScrollBar-bg);
    border-radius: var(--STScrollBar-thumb-border);
    display: block;
}
#menu-tab-item-scrollbar .v-list-group__header  {
    padding-left: 0px!important;
}
#menu-tab-item-scrollbar .v-list-group--sub-group {
    display: block;
}
#menu-tab-item-scrollbar .v-list-group--sub-group {
    display: block;
}
#menu-tab-item-scrollbar .v-list-item > *:not(:first-child) {
    position: relative !important;
    height: auto;
    width: fit-content;
    overflow: hidden;
    clip: rect(1px, 1px, 1px, 1px);
    white-space: nowrap;
    display: initial;
}

.dashboard{
  padding: 0 4px;
  transition: background .2s;
}
.dashboard .v-icon{
  color: var(--Menu-Dashboard-icon-color);
}
.dashboard:hover {
  background: var(--System-Body-bg);
  width: 100%;
  border-radius: 4px;
}

.searchbar{
  width:600px;
}
/* #select .v-select__selections {
    color: #2660A4 !important;
    font-weight:500;
} */
#select{
  max-width:none;
  margin: 0em auto;
  background: var(--System-Top-select-bg);
  border: var(--System-Top-select-border);
  border-radius: 12px;
  display: flex;
}

.selectinput{
  min-width:4.5em;
  align-items: center;
}
#select .v-select__selections input { 
  display: none;
}
#select .v-text-field .v-select__slot .v-select__selection--comma{
  min-width: min-content;
}
  
#select .v-text-field.v-text-field--solo .v-input__control{
    min-height: 10px;
}
#select .v-text-field > .v-input__control > .v-input__slot:after {
    border-width: 0 !important;
}

#select .v-text-field > .v-input__control > .v-input__slot:before {
    display:none;
}
#select .v-text-field.v-input--dense .v-label {
    top: 4px;
    font-weight:400;
    font-size: 14px;
}
#select .v-text-field .v-label--active {
    max-width: 133%;
    transform: translateY(-15px) scale(0.8);
}
.tenantstitleAct .v-text-field .v-label--active{
    left:32px !important;
}
#select .v-text-field__prefix {
    font-weight: 400;
    font-size: 14px;
    color: var(--System-Top-select-color);
}
#select .v-text-field.v-input--dense:not(.v-text-field--outlined) .v-text-field__prefix {
    padding-right: 6px;
}
#select .v-select__selection--comma{
  color: var(--System-Top-select--comma-color);
  font-weight: 500;
}

.badg-num .v-badge__badge{
  background: transparent!important;
  color: #aaa!important;
}
.act-badg-num .v-badge__badge{
  background : #849fb7!important;
  color: #fff!important;
}
@media (max-width:1065px) {
  #top-select{
    display: none!important;
  }
}
</style>