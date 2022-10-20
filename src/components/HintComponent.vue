<template>
    <div>

      <div class="tooltip">Hover over me
        <span class="tooltipcontent">
          <div class="tabbar">
              <v-tabs v-model="tabs" active-class="tabactive" hide-slider>
                <v-tab v-for="item in hinttabs" :key="item.icon" class="tab">
                  <v-icon>{{ item.icon }}</v-icon>
                </v-tab>
              </v-tabs>
            
              <!-- <div v-if="helphelp.show" :style="`position: absolute;z-index:999;top:${helphelp.top};left:${helphelp.left}`">
                  <template v-if="help.html">
                      <iframe :src="fullpath(help.html)" height="100%" width="100%" >
                      </iframe>
                  </template>
                  <template v-else>
                      {{help.text}}
                  </template>
                  <span v-if="help.image!=''"><v-img :src="fullpath(help.image)"  width="350" aspect-ratio="1.7" contain></v-img></span>
              </div> -->
            <v-tabs-items v-model="tabs" style="background: transparent;">
              <v-tab-item>
                  <div id="view" class="tabcontent" v-for="item in hintview" :key="item.key" style="text-align:left;">
                    <!-- <p><b>{{item.key}}</b></p> -->
                    <p>{{item.property.text}}</p>
                    <v-img :src="require(`../assets/${item.property.image}`)"  width="350" aspect-ratio="1.7" contain></v-img>
                  </div>
              </v-tab-item>

              <v-tab-item>
                <div id="edit" class="tabcontent" >
                  <textarea rows="3"></textarea>
                </div>
              </v-tab-item>

              <v-tab-item>
                <div id="html" class="tabcontent">
                  
                </div>
              </v-tab-item>

              <v-tab-item>
                <div id="config" class="tabcontent" style="padding:0px 0px 8px 0px">
                  <table>
                    <tr>
                      <td colspan="2" style="border:0">
                        <span id="hint-file">
                          <v-file-input label="Select A File" solo flat dense hide-details class="file"></v-file-input>
                        </span>
                      </td>
                    </tr>
                    <tr>
                      <td>File name</td>
                      <td><input type="text" id="filename" name="filename" v-model="imgfilename"></td>
                      
                    </tr>
                    <tr>
                      <td>Width</td>
                      <td><input type="text" id="widht" name="width"></td>
                    </tr>
                    <!-- <tr>
                      <td>Height</td>
                      <td><input type="text" id="height" name="height"></td>
                    </tr> -->
                    <tr>
                      <td>Position</td>
                      <td><input type="text" id="position" name="position"></td>
                    </tr>
                    <tr>
                      <td>Background</td>
                      <td><input type="text" id="background" name="background"></td>
                    </tr>
                    </table>
                </div>
              </v-tab-item>
              <button v-if="tabs > 0" type="submit" value="submit" class="hintsave">SAVE</button>
            </v-tabs-items>
          
            </div>
        </span>
      </div>
    
  </div>
</template>
    
    
<script>
  export default {
    data: () => ({
      imgfile:"",
      hinttabs:[{tabname:'VIEW',icon:'mdi-eye-outline'},{tabname:'EDIT',icon:'mdi-playlist-edit'},{tabname:'HTML',icon:'mdi-code-braces'},{tabname:'CONFIG',icon:'mdi-cog-outline'}],
      tabs: null,
      hintview:[{"key":"--System-height", "property" : {"image":"blue.png","text" : "This is a testing"}}]
    }),
    methods:{
      openhint() {
        
      }
    }
  }
</script>

<style>


  *{
    font-family: 'inter';
  }
  .tooltip {
    position: relative;
    display: inline-block;
  }

  .tooltip .tooltipcontent {
    visibility: visible;
    width: 280px;
    height: auto;
    background: #D6E2E6;
    color: #000;
    text-align: center;
    border-radius: 6px;
    position: absolute;
    z-index: 1;
    border: 2px solid #c5cfd2;
  }

  .tooltip:hover .tooltipcontent {
    visibility: visible;
  }

  .tooltip .tooltipcontent::before {
    content: " ";
    position: absolute;
    top: 50px;
    left: 0%;
    margin-left: calc(-8px * 4);
    border-width: 8px;
    border-style: solid;
    border-color:  transparent #D6E2E6 transparent transparent;
    transform: scaleX(3) scaleY(0.8);
  }
  .tooltip .tooltipcontent::after {
    content: " ";
    position: absolute;
    top: 50px;
    right: 0%;
    margin-right: calc(-8px * 4);
    border-width: 8px;
    border-style: solid;
    border-color:  transparent transparent transparent #D6E2E6;
    transform: scaleX(3) scaleY(0.8);
  }

  .tabbar{
    width: 100%;
    overflow: hidden;
    color: #fff!important;
    /* display: flex; */
    justify-content: space-between;
    border-radius: 6px 6px 0 0;
    
  }
  .tabbar .v-slide-group__content{
    width: 100%!important;
  }
  .v-tab{
    min-width: calc(100% / 4)!important;
    padding: 0px 0px!important;
  }
  .tab{
    padding: 0px;
    width: calc(100% / 4)!important;
    border: none;
    /* display: block; */
    outline: 0;
    /* border: 1px solid #eee; */
    border-top: 0px;
    font-size: 12px!important;
    background: #C6D3D7!important;
    color: #A0B2B6!important;
  }
  .tab .v-icon{ 
    color: #A0B2B6!important;
  }
  
  .tabactive{
    background: #D6E2E6!important;
    border-bottom: 0px!important;
  }
  .tabactive .v-icon{
    color: #000!important;
  }
  /* #hint-file .filename{
    width: 70%;
    border-radius: 4px;
    background: #fff;
    border: 0px;
    outline: none;
    padding: 4px;
    font-size: 12px;
    color:#666666;
  }
  #hint-file .filebutton{
    width: 25%;
    border-radius: 4px;
    background: #fff;
    border: 0px;
    outline: none;
    padding: 4px;
    font-size: 12px;
  }
  #hint-file .file{
    filter:alpha(opacity:0);
    opacity:0;
    position:absolute;
    left: 2.5%;
  } */
  #hint-file label{
    font-size: 14px;
  }
  #view p{
    font-size: 14px!important;
    line-height: 20px;
    margin: 0;
  }
  #hint-file .file{
    margin-bottom: 5px;
    padding: 4px!important;
    background: transparent;
  }
  #hint-file .file button{
    background: transparent;
  }
  #config table{
    /* border-collapse: collapse; */
  }
  #config table input{
    width: 90%;
    border-radius: 4px;
    background: #fff;
    border: 0px;
    outline: none;
    padding: 0px 4px;
    font-size: 14px;
  }
  #config table td{
    
    font-size: 14px;
    /* border: 1px solid #C6D3D7; */
  }
  #config table td:first-child{
    width: 40%;
    text-align: left;
    padding-left: 12px;
  }
  .tabcontent{
    color:#000;
    padding: 8px;
  }

  .tabcontent textarea{
    width: 100%;
    outline: none;
    border: 0px;
    border-radius: 4px;
    background: #fff;
  }
  .hintsave{
    color:#000;
    border-radius: 0 0 4px 4px;
    background: #fff;
    border: 0px;
    font-size: 12px;
    width: 100%;
    padding: 8px;
    margin-top: 2px;
  }

</style>