<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <el-row :gutter="20" type="flex" class="row-bg" justify="center">
      <el-col :span="4">
        <el-input placeholder="本金" v-model="input1">
          <template slot="prepend">初始资金</template>
        </el-input>
      </el-col>
      <el-col :span="4">
        <el-input placeholder="复投" v-model="input2">
          <template slot="prepend">复投金额</template>
        </el-input>
      </el-col>
      <el-col :span="4">
        <el-input placeholder="利率" v-model="input3">
          <template slot="prepend">利率</template>
          <template slot="append">%</template>
        </el-input>
      </el-col>
      <el-col :span="4">
        <el-input placeholder v-model="input4">
          <template slot="append">复利次数</template>
        </el-input>
      </el-col>
      <el-col :span="3">
        <el-button type="primary" @click="calculation">计算</el-button>
      </el-col>
    </el-row>

    <div class="table">
      <el-table :data="tableData" style="width: 100%">
        <el-table-column prop="time" label="次数"></el-table-column>
        <el-table-column prop="all" label="总资产"></el-table-column>
        <el-table-column prop="originally" label="本金"></el-table-column>
        <el-table-column prop="profit" label="利润"></el-table-column>
      </el-table>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data() {
    return {
      input1: 200,
      input2: 0,
      input3: 10,
      input4: 12,
      tableData: [],
    };
  },
  methods: {
    calculation() {
      var tableData = [];
      // all 最终收入
      // originally 本金
      // r 年利率
      // n 存了多少年
      // A 复投
      var originally = parseFloat(this.input1) + 0;
      var A = parseFloat(this.input2) + 0;
      var r = parseFloat(this.input3) / 100 + 1;
      var all = originally;
      var n = parseFloat(this.input4) + 0;
      for (var i = 0; i < n; i++) {
        var time = i + 1 + "次";
        all = parseFloat(all * r + A).toFixed(2);
        originally += A;
        var profit = parseFloat(all - originally).toFixed(2);
        tableData.push({
          time,
          all,
          originally,
          profit,
        });
      }
      this.tableData = tableData;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.table {
  padding: 50px 200px;
}
</style>
