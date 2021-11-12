<template>
  <div id="app">
    <header class="header container mx-auto">
      <h1 class="header__tit">農村地方美食小吃特色料理</h1>
    </header>
    <main class="main container mx-auto">
      <Table :data="data[switchIndex]" :startNum="switchIndex * rowSize + 1" />
      <Page :dataLen="data.length" @changePage="switchIndex = $event" />
    </main>
    <Loading :isLoad="isLoad" />
  </div>
</template>

<script>
import Table from '@/components/Table';
import Page from '@/components/Page';
import Loading from '@/components/Loading';

export default {
  name: 'App',
  components: {
    Table,
    Page,
    Loading,
  },
  data() {
    return {
      data: [],
      rowSize: 10,
      switchIndex: 0,
      isLoad: false,
    };
  },
  methods: {
    dataSplit(data) {
      for (let i = 0, len = data.length; i < len; i += this.rowSize) {
        this.data.push(data.slice(i, i + this.rowSize));
      }
      return this.data;
    },
  },
  created() {
    const api = 'https://data.coa.gov.tw/Service/OpenData/ODwsv/ODwsvTravelFood.aspx';
    this.$http.get(api).then((res) => {
      this.data = this.dataSplit(res.data);
    })
      .finally(() => {
        this.isLoad = true;
      });
  },
};
</script>

<style>
body {
  margin: 0;
  font-family: Arial, Helvetica, "微軟正黑體", sans-serif;
  background-color: #fff;
}

img {
  vertical-align: bottom;
}

.container {
  max-width: 890px;
}

.mx-auto {
  margin-left: auto;
  margin-right: auto;
}

.header__tit {
  margin-top: 25px;
  margin-bottom: 25px;
  font-size: 30px;
  text-align: center;
}

.main {
  display: flex;
}
</style>
