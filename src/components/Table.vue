<template>
  <table class="table">
    <thead class="table__head">
      <tr class="table__ls">
        <th class="table__tit table-col1">編號</th>
        <th class="table__tit table-col2">行政區</th>
        <th class="table__tit table-col3">圖片</th>
        <th class="table__tit table-col4">名稱</th>
        <th class="table__tit">介紹</th>
      </tr>
    </thead>
    <tbody class="table__body">
      <tr class="table__ls" v-for="(item, index) in data" :key="item.ID"
        :class="{ 'js-table__ls': index % 2 === 0 ? false : true }">
        <td class="table__item text-center text-gray">{{ startNum + index }}</td>
        <td class="table__item">{{ item.City }}</td>
        <td class="table__item">
          <div class="img__inner">
            <img class="image" :src="item.PicURL" :alt="item.Name">
            <img class="image-hidden" :src="item.PicURL" :alt="item.Name">
          </div>
        </td>
        <td class="table__item text-overflow" v-if="item.Url">
          <a :href="item.Url" target="_blank">{{ item.Name }}</a>
        </td>
        <td class="table__item text-overflow" v-else>{{ item.Name }}</td>
        <td class="table__item">{{ textLimit(item.HostWords) }}</td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  name: 'Table',
  props: {
    data: Array,
    startNum: Number,
  },
  methods: {
    textLimit(text) {
      const len = text.length;
      return len > 50 ? `${text.substring(0, 50)}...` : text;
    },
  },
};
</script>

<style scoped>
.table {
  width: 93%;
  table-layout: fixed;
  border-collapse: collapse;
}

.table__ls:hover {
  background-color: #eff4f7;
}

.table__tit, .table__item {
  box-sizing: border-box;
  padding: 10px;
  font-size: 15px;
  border: 1px solid #ddd;
}

.table__tit {
  color: #707070;
  border-bottom: 2px solid #ccc;
  background: linear-gradient(to bottom, #f7f7f7, #eee);
}

.table__item a {
  color: #3E99C8;
}

.img__inner {
  position: relative;

}

.img__inner .image {
  max-width: 100%;
  height: auto;
}

.img__inner:hover .image-hidden {
  display: block;
}

.image-hidden {
  position: absolute;
  top: 0;
  left: 95px;
  display: none;
  box-sizing: border-box;
  width: 300px;
  border: 10px solid #fff;
  box-shadow: 0 0 5px rgba(0,0,0,.5);
}

.table-col1 {
  width: 55px;
}

.table-col2 {
  width: 70px;
}

.table-col3 {
  width: 100px;
}

.table-col4 {
  width: 160px;
}

.text-center {
  text-align: center;
}

.text-gray {
  color: #999;
}

.text-overflow {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}

.js-table__ls {
  background-color: #f9f9f9;
}
</style>
