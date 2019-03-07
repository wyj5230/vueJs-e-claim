<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <rejectionAlert :tableData="tableData"></rejectionAlert>
    <div>
    <listDown :groups="groups" ></listDown>
    </div>
  </div>
</template>

<script>
  import listDown from './ListDown.vue';
  import rejectionAlert from './RejectionAlert.vue';
  export default {
    name: 'HelloWorld',
    components: {
      listDown,rejectionAlert
    },
    data() {
      return {
        tableData: {
          category: 'taxi',
          amount: '10',
          date: '2016-05-02',
          from: 'MOE SLS',
          to: 'Main Office'
        },
        msg: 'Welcome to Ufinity E-claim System',
        groups: {
          unverified: [{boss: 'pengwai', minion: ['yijie', 'tingwai', 'jackey']}, {
            boss: 'waihong',
            minion: ['jianzhong', 'erwin']
          }, {boss: 'boss3', minion: ['minion1', 'minion2', 'minion3']}]
          , verified:
            [{boss: 'sau long', minion: ['sau jian', 'qiu pei', 'hadi']}, {
              boss: 'coco',
              minion: ['liangliang', 'gou tong']
            }, {boss: 'boss3', minion: ['minion1', 'minion2', 'minion3']}]
          ,
          approved: [{boss: 'xue lei', minion: ['kenny', 'some one']}, {
            boss: 'chee kong',
            minion: ['tharaka', 'sachin']
          }, {boss: 'boss3', minion: ['minion1', 'minion2', 'minion3']}]
        }
      }
    },
    created() {
    },
    methods: {}
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

  h1, h2 {
    font-weight: normal;
  }

  a {
    color: #42b983;
  }

  div {
    vertical-align: middle;
    text-align: center;
  }
</style>
