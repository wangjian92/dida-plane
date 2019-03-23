<template>
  <div class="hello">

    <!-- <div style="border:1px solid red;height: 200px">
      <div style="height: 9%;" v-for="(item, index) in list1" :key="index">
        <div
          style="width:9%;height:100%;border: 1px solid blue;display:inline-block"
          v-for="(row, index) in item.rowEl"
          :class="{'state-init':row.state=='0', 'state-doubt': row.state=='1', 'state-sure': row.state=='2'}"
          :key="index"
          :state="row.state"
          @click="option(row)"
        >
          <el-popover placement="top" width="160" v-model="visible2">
            <p>这是一段内容这是一段内容确定删除吗？</p>
            <div style="text-align: right; margin: 0">
              <el-button size="mini" type="text" @click="visible2 = false">取消</el-button>
              <el-button type="primary" size="mini" @click="visible2 = false">确定</el-button>
            </div>
            <el-button style="padding:0" slot="reference">删除</el-button>
          </el-popover>
        </div>
      </div>
    </div> -->
    <h2 style="color:#409EFF">DIDA PLANE</h2>
    <div style="border:1px solid #42b983;height: auto;">
      <div style="display:flex;padding-left:20px;">
        <div class="widgetBorder green-border" style="width:10%" v-for="(item, index) in row" :key="'row-'+index">{{item}}</div>
      </div>
      <div style="display:flex;height: 10%;" v-for="(item, index) in list1" :key="index">
        <div class="widgetBorder green-border" style="width:20px">{{item.line}}</div>
        <div
          class="widgetBorder"
          v-for="(row, index) in item.rowEl"
          :class="{'state-init':row.state=='0', 'state-doubt': row.state=='1', 'state-sure': row.state=='2'}"
          :key="index"
          :state="row.state"
          @click="option(row)"
        >{{row.state}}</div>
      </div>
    </div>
    <br/>
    <div style="border:1px solid #42b983;height: auto;">
      <div style="display:flex;padding-left:20px;">
        <div class="widgetBorder green-border" style="width:10%" v-for="(item, index) in row" :key="'row-'+index">{{item}}</div>
      </div>
      <div style="display:flex;height: 9%;" v-for="(item, index) in list2" :key="index">
        <div class="widgetBorder green-border" style="width:20px">{{item.line}}</div>
        <div
          class="widgetBorder"
          v-for="(row, index) in item.rowEl"
          :class="{'state-init':row.state=='0', 'state-doubt': row.state=='1', 'state-sure': row.state=='2'}"
          :key="index"
          :state="row.state"
          @click="option(row)"
        >{{row.state}}</div>
      </div>
    </div>
    <br/>
    <el-button @click="resetFun">重置</el-button>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      visible2: false,
      list1: [],
      list2: [],
      state: ['0', '1', '2'],
      row: ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9'],
      line: ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J']
    }
  },
  computed: {
    list: function () {
      const lineTemp = []
      // const rowTemp = []
      for (let l = 0; l < this.line.length; l++) {
        lineTemp.push({
          line: this.line[l],
          rowEl: []
        })
        for (let r = 0; r < this.row.length; r++) {
          const rowElement = { rowNo: this.row[r], state: this.state[0] }
          lineTemp[l].rowEl.push(rowElement)
        }
      }
      return lineTemp
    }
  },
  mounted () {
    this.$nextTick(() => {
      this.init()
    })
  },
  methods: {
    init () {
      this.list1 = JSON.parse(JSON.stringify(this.list))
      this.list2 = JSON.parse(JSON.stringify(this.list))
    },
    resetFun () {
      this.init()
    },
    option (item) {
      switch (item.state) {
        case '0':
          item.state = '1'
          break
        case '1':
          item.state = '2'
          break
        case '2':
          item.state = '0'
          break

        default:
          break
      }
      this.$forceUpdate()
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
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
.green-border {
  color: #ffffff;
  background-color: #99df77;
  border: 1px solid #42b983!important;
}
.state-init {
  background-color: #ffffff;
}
.state-doubt {
  background-color: #a1a1a1;
}
.state-sure {
  background-color: #67C23A;
}
.widgetBorder {
  width:10%;height:100%;border: 1px solid #409EFF;display:inline-block;
}
</style>
