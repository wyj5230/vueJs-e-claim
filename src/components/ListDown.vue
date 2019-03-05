<template>
  <el-container>
    <el-aside>
      <div class="content">
        <div class="tabs">
          <a v-on:click="activetab=1;showImage=false" v-bind:class="[ activetab === 1 ? 'active' : '' ]">Tab 1</a>
          <a v-on:click="activetab=2;showImage=false" v-bind:class="[ activetab === 2 ? 'active' : '' ]">Tab 2</a>
          <a v-on:click="activetab=3;showImage=false" v-bind:class="[ activetab === 3 ? 'active' : '' ]">Tab 3</a>
        </div>
        <div v-if="activetab === 1" class="tabcontent">
          <el-menu >
            <el-submenu v-for="(group,unverifiedIndex) in groups.unverified" :index="'1-'+unverifiedIndex" >
              <template slot="title"><span class="bold">{{group.boss}}({{group.minion.length}})</span></template>
              <el-menu-item-group >
                <el-menu-item class="border" v-for="(minion,unverifiedChildIndex) in group.minion"
                              :index="'1-'+unverifiedIndex+'-'+unverifiedChildIndex" @click="showHideImage(minion)">
                  <template slot="title">{{minion}}</template>
                </el-menu-item>
              </el-menu-item-group>
            </el-submenu>
          </el-menu>
        </div>
        <div v-if="activetab === 2" class="tabcontent">
          <el-menu>
            <el-submenu v-for="(group,verifiedIndex) in groups.verified" :index="'2-'+verifiedIndex">
              <template slot="title"><span class="bold">{{group.boss}}({{group.minion.length}})</span></template>
              <el-menu-item-group>
                <el-menu-item v-for="(minion,verifiedChildIndex) in group.minion"
                              :index="'2-'+verifiedIndex+'-'+verifiedChildIndex">
                  <template slot="title">{{minion}}</template>
                </el-menu-item>
              </el-menu-item-group>
            </el-submenu>
          </el-menu>
        </div>
        <div v-if="activetab === 3" class="tabcontent">
          <el-menu>
            <el-submenu v-for="(group,approvedIndex) in groups.approved" :index="'3-'+approvedIndex">
              <template slot="title"><span class="bold">{{group.boss}}({{group.minion.length}})</span></template>
              <el-menu-item-group>
                <el-menu-item v-for="(minion,approvedChildIndex) in group.minion"
                              :index="'3-'+approvedIndex+'-'+approvedChildIndex">
                  <template slot="title">{{minion}}</template>
                </el-menu-item>
              </el-menu-item-group>
            </el-submenu>
          </el-menu>
        </div>
      </div>
    </el-aside>
    <el-container v-if="showImage">
      <el-main>
        <img :src="getImgUrl(currentPic)" v-bind:alt="currentPic" height="550"/>
      </el-main>
    </el-container>
  </el-container>
</template>

<script>
  export default {
    name: "listDown",
    props: ['groups', 'activetabProp','showImageProp'],
    data() {
      return {
        activetab: this.activetabProp,
        showImage: this.showImageProp,
        currentPic: ''
      }
    },
    methods: {
      showHideImage(minion) {
        this.showImage = true;
        this.currentPic = minion;
      },
      getImgUrl(currentPic) {
        if (!this.currentPic){
          return
        }
        return require('../assets/'+currentPic+'.png')
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
    margin: 0;
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
    overflow: hidden;
    margin-left: 20px;
    margin-bottom: -2px; // hide bottom border
  }

  .tabs ul {
    list-style-type: none;
    margin-left: 20px;
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
    background-color: #fff;
    color: #484848;
    border-bottom: 2px solid #fff;
    cursor: default;
  }

  /* Style the tab content */
  .tabcontent {
    padding: 30px;
    box-shadow: 3px 3px 6px #e1e1e1
  }

  .bold {
    font-weight: bold;
    font-size: medium;
    font-family: Montserrat;
  }

  .border {
    border-up:1px solid black;
    border-bottom:1px solid black;
  }

</style>
