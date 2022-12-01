<template>
<div>
    <div id="main" style="display:flex">
        <div style="display:block;" id="cards">
            <div class="cards">
                <v-row>
                    <v-col cols="5">
                        <v-card class="tab-card">
                            <v-list-item class="tab-card-content">
                                <v-list-item-content>
                                    <div class="tab-card-content-title">User</div>
                                    <v-divider></v-divider>
                                </v-list-item-content>
                            </v-list-item>
                        </v-card>
                    </v-col>
                    <v-col cols="7">
                        <v-card class="tab-card">
                            <v-list-item class="tab-card-content">
                                <v-list-item-content>
                                    <div class="tab-card-content-title">Menu Control
                                        <v-spacer></v-spacer><v-icon right>mdi-numeric-6-circle</v-icon>
                                    </div>
                                    <v-divider></v-divider>
                                </v-list-item-content>
                            </v-list-item>
                        </v-card>
                    </v-col>
                </v-row>
            </div>
            <div class="cards">
                <v-row>
                    <v-col cols="12">
                    <v-card class="tab-card">
                        <v-list-item class="tab-card-content">
                            <v-list-item-content>
                                <div class="tab-card-content-title">Menu Control
                                    <v-spacer></v-spacer><v-icon right @click="showCompanyDetail()">mdi-circle-edit-outline</v-icon>
                                </div>
                                <v-divider></v-divider>
                            </v-list-item-content>
                        </v-list-item>
                    </v-card>
                </v-col>
                </v-row>
            </div>
        </div>
        <div id="dcard">
            <v-card class="detail-card">
                <v-list-item class="tab-card-content">
                    <v-list-item-content>
                        <div class="tab-card-content-title">
                            <v-spacer></v-spacer><v-icon right @click="closeCompanyDetail()">mdi-close</v-icon>
                        </div>
                        <!-- <div style="border: 1px solid #ccc; margin-top: 10px">
                            <Toolbar style="border-bottom: 1px solid #ccc" :editor="editor" :defaultConfig="toolbarConfig"/>
                            <Editor style="height: 400px; overflow-y: hidden" :defaultConfig="editorConfig" v-model="html" @onCreated="onCreated"/>
                        </div> -->
                    </v-list-item-content>
                </v-list-item>
            </v-card>
        </div>
    </div>

</div>
</template>


<script>
// import { Editor, Toolbar } from "@wangeditor/editor-for-vue";
// import StepDetail from './StepDetail.vue';
    export default {
    // components: { StepDetail },
    // components: { Editor, Toolbar },
    data: () => ({
        tabs: 1,
        resultsetbody:[{tabname:'Property',icon:'mdi-cog'},{tabname:'SQL',icon:'mdi-database'},{tabname:'Ask',icon:'mdi-table-key'}],

        toolbarConfig: {
            toolbarKeys: [
            'bold', 'headerSelect','fontSize' ,'fontFamily', 'color'
            ],
            // excludeKeys: [ /* 隐藏哪些菜单 */ ],
        },
        editorConfig: {
            placeholder: "请输入内容...",
            // autoFocus: false,
            // 所有的菜单配置，都要在 MENU_CONF 属性下
            MENU_CONF: {
                insertImage: {
                    onInsertedImage (imageNode) {
                        if(imageNode == null) return
                        
                        const {src, alt, url, href} = imageNode;
                        console.log('inserted Image', src, alt, url, href)
                    }
                },
                uploadImage: {
                    // server: 'url', /* server's url, essential */
                    base64LimitSize: 1024 * 1024, // if file size is less than this, use base64 instead of server 
                    maxFileSize: 3 * 1024 * 1024, // default is 2MB
                }
            },
        },
        
    }),
    methods:{
        showCompanyDetail(){
            // var cards = document.getElementsByClassName('cards')
            var cards = document.getElementById('cards')
            var dcard = document.getElementById('dcard')
            // for(var i = 0; i < cards.length; i++){
            //     cards[i].style.width = "70%"
            // }
            cards.style.width= "69.5%"
            dcard.style.width = "29.5%"
        },
        closeCompanyDetail(){
            var cards = document.getElementById('cards')
            var dcard = document.getElementById('dcard')
            cards.style.width= "100%"
            dcard.style.width = "0%"
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
    padding-left: 52px;
    margin: 12px 12px;
}
#cards{
    width: 100%;
    transition: .5s;
}
.cards{
    width: 100%;
}
.tab-card{
  font-size: 16px;
  min-height: 20vh;
  box-shadow: 0px 3px 18px rgba(68,67,67,.05)!important;
  background: #fff!important;
  border-radius: 12px!important;
  margin-bottom: 15px;
}
.tab-card-content{
  padding: 0;
}
.tab-card-content-title{
  font-size: 20px;
  padding: 5px 20px;
  margin-bottom: 0;
  font-weight: 600;
  display: flex;
  align-items: center;
}
.tab-card .v-list-item__content{
  padding: 0px!important;
  margin: 0;
}
#dcard{
    width: 0%;
    margin-left: 1%;
    transition: .5s;
}
.detail-card{
    font-size: 16px;
    min-height: calc(100% - 24px);
    box-shadow: 0px 3px 18px rgba(68,67,67,.05)!important;
    background: #fff!important;
    border-radius: 12px!important;
    margin-bottom: 15px;
    width: 100%;
}
</style>
<style src="@wangeditor/editor/dist/css/style.css"></style>