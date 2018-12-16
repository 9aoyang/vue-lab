<template>
  <div>
    <el-button @click="dialogVisible = true">选择</el-button>
    <el-dialog
      title="选择人员"
      :visible.sync="dialogVisible"
      :close-on-click-modal="false"
      :before-close="handleClose">
      <section class="main">
        <div>
          <el-input v-model="input" placeholder="请输入组织"></el-input>
          <el-tree
            :props="props"
            :load="loadNode"
            lazy>
          </el-tree>
        </div>
        <div>
          <span>
            <el-checkbox v-model="checked">包括下级组织</el-checkbox>
            <el-input
              placeholder="请输入人员姓名"
              suffix-icon="el-icon-search"
              v-model="input21">
            </el-input>
          </span>
          <el-table
            :data="tableData"
            style="width: 100%">
            <el-table-column
              prop="date"
              label="日期"
              width="180">
            </el-table-column>
            <el-table-column
              prop="name"
              label="姓名"
              width="180">
            </el-table-column>
            <el-table-column
              prop="address"
              label="地址">
            </el-table-column>
          </el-table>
          <el-pagination
            background
            layout="prev, pager, next"
            :total="1000">
          </el-pagination>
        </div>
      </section>
      <span slot="footer" class="dialog-footer">
        <el-button @click="dialogVisible = false">取 消</el-button>
        <el-button type="primary" @click="dialogVisible = false">确 定</el-button>
      </span>
    </el-dialog>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      input: '',
      dialogVisible: false,
      props: {
        label: 'name',
        children: 'zones',
        isLeaf: 'leaf',
      },
      tableData: [{
        date: '2016-05-02',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1518 弄'
      }, {
        date: '2016-05-04',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1517 弄'
      }, {
        date: '2016-05-01',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1519 弄'
      }, {
        date: '2016-05-03',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1516 弄'
      }]
    };
  },
  methods: {
    handleClose(done) {
      this.$confirm('确认关闭？')
        .then(_ => {
          done();
        })
        .catch(_ => {});
    },
    loadNode(node, resolve) {
      if (node.level === 0) {
        return resolve([{ name: 'region' }]);
      }
      if (node.level > 1) return resolve([]);

      setTimeout(() => {
        const data = [{
          name: 'leaf',
          leaf: true
        }, {
          name: 'zone'
        }];

        resolve(data);
      }, 500);
    }
  },
  props: {
    msg: String
  }
};
</script>
<style scoped>

</style>
