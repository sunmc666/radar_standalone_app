<template>
  <div class="animated bounceInUp">
    <h3>数据记录</h3>
     <!-- <table>
      <tr class="text">
        <td class="tab">Index</td>
        <td class="tab">横坐标X</td>
        <td class="tab">纵坐标Y</td>
      </tr>
      <tr class="text" 
          v-for="(dots,index) in List"
          :key="index">
        <td class="tab">{{index}}</td>
        <td class="tab">{{dots.x}}</td>
        <td class="tab">{{dots.y}}</td>
      </tr>
    </table> -->
    <el-table
    :data="List"
    style="width: 100%"
    :default-sort = "{prop: 'index', order: 'ascending'}"
    >
    <el-table-column
      prop="index"
      label="Index"
      sortable
      width="180">
      <template slot-scope="scope">
        <span>{{scope.row.index}}</span>
      </template>
    </el-table-column>

    <el-table-column
      prop="x"
      label="横坐标 X"
      width="180">
      <template slot-scope="scope">
        <span>{{scope.row.x}}</span>
      </template>
    </el-table-column>
    <el-table-column
      prop="y"
      label="纵坐标 Y"
     >
      <template slot-scope="scope">
        <span>{{scope.row.y}}</span>
      </template>
    </el-table-column>
  </el-table>
  </div>
</template>

<script>
export default {
  data () {
    return {
      List: []
    }
  },
  mounted () {
    window.eventBus.$on('dot', (arg) => {
      console.log(arg)
      var msg = {index: 0, x: '', y: ''}
      if (msg.x !== arg.x) {
        msg.x = arg.x
        msg.y = arg.y
        msg.index = this.List.length + 1
        this.List.push(msg)
      }
    })
  }
}
</script>