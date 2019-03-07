<template>
  <el-container>
      <div class="content">
        <div class="tabs">
          <a v-on:click="activetab=1;showImage=false" v-bind:class="[ activetab === 1 ? 'active' : '' ]">Unverified</a>
          <a v-on:click="activetab=2;showImage=false" v-bind:class="[ activetab === 2 ? 'active' : '' ]">Verified</a>
          <a v-on:click="activetab=3;showImage=false" v-bind:class="[ activetab === 3 ? 'active' : '' ]">Approved</a>
        </div>
        <div v-if="activetab === 1" class="tabcontent">
          <vue-custom-scrollbar class="scroll-area" settings='maxScrollbarLength: 30'>
            <el-menu>
              <el-submenu v-for="(group,unverifiedIndex) in groups.unverified" :index="'1-'+unverifiedIndex">
                <template slot="title"><span class="bold ">{{group.boss}}({{group.minion.length}})</span><i
                  class='el-icon-question'></i></template>

                <el-menu-item class="border" v-for="(minion,unverifiedChildIndex) in group.minion"
                              :index="'1-'+unverifiedIndex+'-'+unverifiedChildIndex" @click="showHideImage(minion)">
                  <template slot="title">{{minion}}<i class='el-icon-arrow-right arrow'></i></template>
                </el-menu-item>
              </el-submenu>
            </el-menu>
          </vue-custom-scrollbar>
        </div>
        <div v-if="activetab === 2" class="tabcontent">
          <vue-custom-scrollbar class="scroll-area" settings='maxScrollbarLength: 30'>
            <el-menu>
              <el-submenu v-for="(group,verifiedIndex) in groups.verified" :index="'2-'+verifiedIndex">
                <template slot="title"><span class="bold">{{group.boss}}({{group.minion.length}})</span></template>
                <el-menu-item class="border" v-for="(minion,verifiedChildIndex) in group.minion"
                              :index="'2-'+verifiedIndex+'-'+verifiedChildIndex">
                  <template slot="title">{{minion}}<i class='el-icon-arrow-right arrow'></i></template>
                </el-menu-item>
              </el-submenu>
            </el-menu>
          </vue-custom-scrollbar>
        </div>
        <div v-if="activetab === 3" class="tabcontent">
          <vue-custom-scrollbar class="scroll-area" settings='maxScrollbarLength: 30'>
            <el-menu>
              <el-submenu v-for="(group,approvedIndex) in groups.approved" :index="'3-'+approvedIndex">
                <template slot="title"><span class="bold">{{group.boss}}({{group.minion.length}})</span></template>
                <el-menu-item class="border" v-for="(minion,approvedChildIndex) in group.minion"
                              :index="'3-'+approvedIndex+'-'+approvedChildIndex">
                  <template slot="title">{{minion}}<i class='el-icon-arrow-right arrow'></i></template>
                </el-menu-item>
              </el-submenu>
            </el-menu>
          </vue-custom-scrollbar>
        </div>
      </div>
    <div v-if="showImage">
      <img :src="getImgUrl(currentPic)" height="550"/>
    </div>
    <div class="claimpicture" v-if="!showImage">
      <span>Please click on a staff to view his or her claims.</span>
    </div>
  </el-container>
</template>

<script>
  import vueCustomScrollbar from 'vue-custom-scrollbar'

  export default {
    name: "listDown",
    props: ['groups'],
    components: {
      vueCustomScrollbar
    },
    data() {
      return {
        activetab: 1,
        showImage: false,
        currentPic: ''
      }
    },
    methods: {
      showHideImage(minion) {
        this.showImage = true;
        this.currentPic = minion;
      },
      getImgUrl(currentPic) {
        if (!this.currentPic) {
          return
        }
        return require('../assets/' + currentPic + '.png')
      }
    },

  }
</script>

<style scoped lang="scss">
  /* Import Google Font */
  @import url(https://fonts.googleapis.com/css?family=Nunito+Sans);

  /* RESET */
  * {
    box-sizing: border-box;
    padding: 0;
  }

  /* STYLING */
  .container {
    max-width: 620px;
    min-width: 420px;
    margin: 40px auto;
    font-family: "Nunito Sans", Arial, Helvetica, sans-serif;
    color: #888;
  }

  /* Style the tabs */
  .tabs {
    margin-left: 30px;
  }

  .tabs ul {
    list-style-type: none;
    margin-left: 30px;
  }

  .tabs a {
    float: left;
    cursor: pointer;
    padding: 12px 24px;
    transition: background-color 0.2s;
    border: 1px solid #ccc;
    border-right: none;
    background-color: #f1f1f1;
    border-radius: 10px 10px 0 0;
    font-weight: bold;
    color: #aaa;
  }

  .tabs a:last-child {
    border-right: 1px solid #ccc;
  }

  /* Change background color of tabs on hover */
  .tabs a:hover {
    background-color: #aaa;
    color: #fff;
  }

  /* Styling for active tab */
  .tabs a.active {
    background-color: #004087;
    color: #fff;
    border-bottom: 2px solid #fff;
    cursor: default;
  }

  /* Style the tab content */
  .tabcontent {
    padding: 30px;
  }

  .bold {
    font-weight: bold;
    font-size: medium;
    font-family: Montserrat;
  }

  .border {
    border-left: 1px solid;
    border-right: 1px solid;
    border-bottom: 1px solid;
    border-top: 1px solid;
  }

  .scroll-area {
    position: relative;
    margin: auto;
    width: 450px;
    height: 500px;
  }

  .arrow {
    float: right;
    padding-top: 16px;
  }

  .el-submenu {
    box-shadow: 0 2px 4px rgba(0, 0, 0, .12), 0 0 6px rgba(0, 0, 0, .04);
    border: 2px solid;
  }

  .i {
    font-size: 15px;
  }

  .claimpicture {
    text-align: center;
    width: 1000px;
    height: 700px;
    border: 2px dashed #f69c55;
    line-height: 700px;
  }

  span {
    display: inline-block;
    vertical-align: middle;
    line-height: normal;
  }
</style>
