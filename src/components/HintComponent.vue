<template>
    <div>
      <div class="tooltip">Hover over me
        <span class="tooltipcontent">
          <div class="tabbar">
              <v-tabs v-model="tabs" active-class="tabactive" hide-slider>
                <v-tab v-for="item in hinttabs" :key="item" class="tab">
                  {{ item }}
                </v-tab>
              </v-tabs>
            

            <v-tabs-items v-model="tabs" style="padding:8px">
              <v-tab-item >
                  <div id="view"  class="tabcontent" style="text-align:left;padding-left:12px">
                    <img>
                    <p>Background of the System Background of the System</p>
                  </div>
              </v-tab-item>

              <v-tab-item>
                <div id="edit" class="tabcontent" >
                  <textarea rows="3"></textarea>
                  <button type="submit" value="submit">SUBMIT</button>
                </div>
              </v-tab-item>

              <v-tab-item>
                <div id="html" class="tabcontent">
                  <textarea rows="3"></textarea>
                  <button type="submit" value="submit">SAVE</button>
                </div>
              </v-tab-item>

              <v-tab-item>
                <div id="config" class="tabcontent">
                  <table>
                    <tr>
                      <td colspan="2">
                        <span id="hint-file">
                          <v-file-input label="File input" solo flat dense hide-details class="file"></v-file-input>
                          <!-- <input type="text" id="filename" name="filename" class="filename">
                          <input type="button" class="filebutton" value="選取檔案 ">
                          <input type="file" id="file" name="file" class="file" onchange="document.getElementById('filename').value = this.value"> -->
                        </span>
                      </td>
                    </tr>
                    <tr>
                      <td>Position</td>
                      <td><input type="text" id="position" name="position"></td>
                    </tr>
                    <tr>
                      <td>Width</td>
                      <td><input type="text" id="widht" name="width"></td>
                    </tr>
                    <tr>
                      <td>Height</td>
                      <td><input type="text" id="height" name="height"></td>
                    </tr>
                    <tr>
                      <td>Background</td>
                      <td><input type="text" id="background" name="background"></td>
                    </tr>
                    <tr>
                      <td colspan="2"><button type="submit" value="submit">SUBMIT</button></td>
                    </tr>
                    </table>
                </div>
              </v-tab-item>
            </v-tabs-items>
          
            </div>
        </span>
      </div>
    
  </div>
</template>
    
    
<script>
  export default {
    data: () => ({
      hinttabs:['VIEW','EDIT','HTML','CONFIG'],
      tabs: null,
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
  }

  .tooltip:hover .tooltipcontent {
    visibility: visible;
  }

  .tooltip .tooltipcontent::before {
    content: " ";
    position: absolute;
    top: 50%;
    left: 0%;
    margin-left: -16px;
    border-width: 8px;
    border-style: solid;
    border-color:  transparent #D6E2E6 transparent transparent;
  }
  .tooltip .tooltipcontent::after {
    content: " ";
    position: absolute;
    top: 50%;
    right: 0%;
    margin-right: -16px;
    border-width: 8px;
    border-style: solid;
    border-color:  transparent transparent transparent #D6E2E6;
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
    padding: 8px 0px!important;
  }
  .tab{
    padding: 8px;
    width: calc(100% / 4)!important;
    border: none;
    /* display: block; */
    outline: 0;
    border: 1px solid #eee;
    border-top: 0px;
    font-size: 12px!important;
    background: #C6D3D7!important;
    color: #A0B2B6!important;
  }
  
  .tabactive{
    background: #D6E2E6!important;
    color: #000!important;
    border-bottom: 0px!important;
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
  #hint-file .file{
    margin-bottom: 5px;
    padding: 4px!important;
  }
  #hint-file .file button{
    background: transparent;
  }
  table input{
    width: 90%;
    border-radius: 4px;
    background: #fff;
    border: 0px;
    outline: none;
    padding: 2px 4px;
    font-size: 14px;
  }
  table td{
    width: 50%;
    font-size: 14px;
  }
  .tabcontent{
    color:#000;
  }
  .tabcontent button{
    color:#000;
    border-radius: 4px;
    background: #fff;
    border: 0px;
    font-size: 12px;
    width: 100%;
    padding: 4px;
    margin-top: 5px;
  }
  .tabcontent textarea{
    width: 95%;
    outline: none;
    border: 0px;
    border-radius: 4px;
    background: #fff;
  }

</style>