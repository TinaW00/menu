<template>
    <div>
        <div v-if="step.key == 'property'">{{step.key}}
            <v-tabs v-model="tabs" class="resultset-tabs" hide-slider background-color="transparent">
                <!-- <v-hover v-slot="{ hover }"> -->
                <v-tab v-for="item in PropertyTabs" :key="item.tabname" class="resultset-tab"  active-class="resultset-tab-act" :ripple="false">
                    <v-icon left>{{ item.icon }}</v-icon>{{item.tabname}}
                </v-tab>
                <!-- </v-hover> -->
            </v-tabs>
            <v-tabs-items v-model="tabs" style="background: transparent;padding: 0 5px 20px 0px;">
                <v-tab-item>
                    <v-card class="tab-property-card">
                        <v-list-item class="tab-property-card-content">
                            <v-list-item-content>
                                <div class="tab-card-content-title">
                                    <!-- <v-icon left>mdi-menu</v-icon> -->
                                    Property<v-spacer></v-spacer>
                                    <span style="float:right">
                                    <v-icon right>mdi-format-font-size-increase</v-icon>
                                    </span>
                                </div>
                                <v-divider></v-divider>
                            </v-list-item-content>
                        </v-list-item>
                    </v-card>
                </v-tab-item>
                <v-tab-item>
                    <v-card class="tab-card">
                        <v-list-item class="tab-card-content">
                            <v-list-item-content>
                                <div class="tab-card-content-title">
                                    <!-- <v-icon left>mdi-menu</v-icon> -->
                                    SQL<v-spacer></v-spacer>
                                    <span style="float:right">
                                    <v-icon right>mdi-format-font-size-increase</v-icon>
                                    <!-- <v-icon right>mdi-database-check</v-icon>
                                    <v-icon right>mdi-magnify</v-icon> -->
                                    </span>
                                </div>
                                <v-divider></v-divider>
                                <textarea class="tab-card-content-text" placeholder=""></textarea>
                            </v-list-item-content>
                        </v-list-item>
                    </v-card>
                    <!-- <v-card class="tab-card tab-card-JsonEditor">
                    <v-list-item class="tab-card-content">
                        <v-list-item-content>
                            <div class="tab-card-content-title">
                            <v-icon left>mdi-menu</v-icon>Ask<v-spacer></v-spacer>
                            <span style="float:right">
                                <v-icon right>mdi-format-font-size-increase</v-icon>
                                <v-icon right>mdi-magnify</v-icon>
                            </span>
                            </div>
                            <v-divider></v-divider>
                            <v-data-table :headers="JsonEditorHeaders" :items="JsonEditorItem" item-key="name" :items-per-page="5">
                            
                            <template v-slot:item.calories="{ item }">
                                <v-icon :color="getColor(item.calories)" dark>
                                {{ item.calories }}
                                </v-icon>
                            </template> 

                            </v-data-table>
                        </v-list-item-content>
                    </v-list-item>
                    </v-card> -->
                </v-tab-item>
                <v-tab-item>
                    <v-card class="tab-property-card">
                        <v-list-item class="tab-property-card-content">
                            <v-list-item-content>
                                <div class="tab-card-content-title">
                                    <!-- <v-icon left>mdi-menu</v-icon> -->
                                    Ask<v-spacer></v-spacer>
                                    <span style="float:right">
                                    <v-icon right>mdi-format-font-size-increase</v-icon>
                                    </span>
                                </div>
                                <v-divider></v-divider>
                            </v-list-item-content>
                        </v-list-item>
                    </v-card>
                </v-tab-item>
            </v-tabs-items>
        </div>
        <div v-if="step.key == 'sqlResult'">{{step.key}}
            <v-tabs v-model="tabs" class="resultset-tabs" hide-slider background-color="transparent">
                <!-- <v-hover v-slot="{ hover }"> -->
                <v-tab v-for="item in SqulResultTabs" :key="item.tabname" class="resultset-tab"  active-class="resultset-tab-act" :ripple="false">
                    <v-icon left>{{ item.icon }}</v-icon>{{item.tabname}}
                </v-tab>
                <!-- </v-hover> -->
            </v-tabs>
            <v-tabs-items v-model="tabs" style="background: transparent;padding: 0 5px 20px 0px;">
                <v-tab-item>
                    <v-card class="tab-card">
                        <v-list-item class="tab-card-content">
                            <v-list-item-content>
                                <div class="tab-card-content-title">
                                    <!-- <v-icon left>mdi-menu</v-icon> -->
                                    Final SQL<v-spacer></v-spacer>
                                    <span style="float:right">
                                    <v-icon right>mdi-format-font-size-increase</v-icon>
                                    </span>
                                </div>
                                <v-divider></v-divider>
                                <textarea class="tab-card-content-text" placeholder=""></textarea>
                            </v-list-item-content>
                        </v-list-item>
                    </v-card>
                </v-tab-item>
                <v-tab-item>
                    <v-card class="tab-card">
                        <v-list-item class="tab-card-content">
                            <v-list-item-content>
                                <div class="tab-card-content-title">
                                    <!-- <v-icon left>mdi-menu</v-icon> -->
                                    Json<v-spacer></v-spacer>
                                    <span style="float:right">
                                    <v-icon right>mdi-format-font-size-increase</v-icon>
                                    </span>
                                </div>
                                <v-divider></v-divider>
                                <textarea class="tab-card-content-text" placeholder=""></textarea>
                            </v-list-item-content>
                        </v-list-item>
                    </v-card>
                </v-tab-item>
            </v-tabs-items>
        </div>
    </div>
</template>

<script>
 export default {
    props :['step'],
    data: () => ({
      tabs: 0,
      stepnow:1,
      PropertyTabs:[{tabname:'Property',icon:'mdi-cog'},{tabname:'SQL',icon:'mdi-database'},{tabname:'Ask',icon:'mdi-table-key'}],
      SqulResultTabs:[{tabname:'Final SQL',icon:'mdi-database-check'},{tabname:'Json',icon:'mdi-text-long'}],
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
    })
 }
</script>
<style scoped>
.resultset-tabs .v-slide-group__content {
    /* justify-content: end; */
    /* margin-left: 20px; */
    align-items: center;
}
.resultset-tab {
    /* color: #000!important; */
    background: transparent;
    margin: 0 0px!important;
    padding: 12px 20px;
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
  border-radius: 0 12px 12px 12px!important;
}
.withouttab-property-card{
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
  border-radius: 0 12px 12px 12px!important;
  margin-bottom: 15px;
}
.withouttab-card{
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
.tab-card-content-title .v-icon{
  color: #A0B2B6;
  font-weight: 400;
}
.tab-card-content-text{
  padding: 8px;
  outline: none;
  min-height: calc(20vh - 40px);
}
.tab-property-card .v-list-item, .tab-card .v-list-item{
  min-height: auto;
}
.tab-property-card .v-list-item__content, .tab-card .v-list-item__content{
  padding: 0px!important;
  margin: 0;
}
.tab-property-card .v-list-item__content > *:not(:last-child), .tab-card .v-list-item__content > *:not(:last-child){
  margin: 0;
}
</style>