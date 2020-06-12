<template>
  <div class="about">
    <el-table ref="multipleTable" border :span-method="objectSpanMethod" :cell-class-name="tableRowClassName"
              @cell-mouse-leave="cellMouseLeave"  @cell-mouse-enter="cellMouseEnter" :data="tableData" style="width: 80%;margin:0 auto;">
      <el-table-column label="商品类别" prop="productType" align="center"></el-table-column>
      <el-table-column label="商品价格" prop="price" align="center"></el-table-column>
      <el-table-column label="商品名称" prop="productName" width="180px" align="center"></el-table-column>
      <el-table-column label="操作人员" prop="operator"  align="center"></el-table-column>
      <el-table-column label="更新时间" prop="updateTime" align="center">
      </el-table-column>
    </el-table>
  </div>
</template>
<script>
  export default {
    name:'About',
    data(){
      return {
        tableData: [
          {
            productType: "纺织品",
            price: 123,
            productName: '男装上衣',
            amount: 20,
            operate_number: "20180831142020",
            price: "36.00",
            updateTime: "2018-08-31",
            operator: "小吴"
          },{
            productType: "纺织品",
            price: 123,
            productName: '男装裤子',
            amount: 20,
            operate_number: "20180831142020",
            price: "36.00",
            updateTime: "2018-08-31",
            operator: "小吴"
          },{
            productType: "饮料",
            price: 123,
            productName: '康师傅冰红茶',
            amount: 20,
            operate_number: "20180823142020",
            price: "36.00",
            updateTime: "2018-08-31",
            operator: "小吴"
          },{
            productType: "纺织品",
            price: 223,
            productName: '男装裤子',
            amount: 10,
            operate_number: "20180821142020",
            price: "36.00",
            updateTime: "2018-08-31",
            operator: "小王"
          },{
            productType: "绸缎",
            price: 888,
            productName: '旗袍',
            amount: 200,
            operate_number: "20180821142020",
            price: "36.00",
            updateTime: "2018-08-31",
            operator: "小吴"
          },{
            productType: "绸缎",
            price: 123,
            productName: '席子',
            amount: 20,
            operate_number: "20180821142020",
            price: "36.00",
            updateTime: "2018-08-31",
            operator: "小吴"
          },
        ],
        rowIndex: '-1',
        OrderIndexArr: [],
        hoverOrderArr: []
      }
    },
    mounted() {
      this.getOrderNumber()
    },
    methods:{
      getOrderNumber() {
        let OrderObj = {};
        this.tableData.forEach((element, index) => {
          element.rowIndex = index
          if (OrderObj[element.operate_number]) {
            OrderObj[element.operate_number].push(index);
          } else {
            OrderObj[element.operate_number] = [];
            OrderObj[element.operate_number].push(index);
          }
        });
        // 将数组长度大于1的值 存储到this.OrderIndexArr（也就是需要合并的项）
        for (let k in OrderObj) {
          if (OrderObj[k].length > 1) {
            this.OrderIndexArr.push(OrderObj[k])
          }
        }
      },
      // 合并单元格
      objectSpanMethod({row,column,rowIndex,columnIndex}) {
        if (columnIndex === 0 || columnIndex === 3 || columnIndex === 4) {
          for (let i = 0; i < this.OrderIndexArr.length; i++) {
            let element = this.OrderIndexArr[i]
            for (let j = 0; j < element.length; j++) {
              let item = element[j]
              if (rowIndex == item) {
                if (j == 0) {
                  return {
                    rowspan: element.length,
                    colspan: 1
                  }
                } else if (j != 0) {
                  return {
                    rowspan: 0,
                    colspan: 0
                  }
                }
              }
            }
          }
        }
      },
      tableRowClassName({row,rowIndex}) {
        let arr = this.hoverOrderArr
        for (let i = 0; i < arr.length; i++) {
          if (rowIndex == arr[i]) {
            return 'hovered-row'
          }
        }
      },
      cellMouseEnter(row, column, cell, event) {
        this.rowIndex = row.rowIndex;
        this.hoverOrderArr = [];
        this.OrderIndexArr.forEach(element => {
          if (element.indexOf(this.rowIndex) >= 0) {
            this.hoverOrderArr = element
          }
        })
      },
      cellMouseLeave(row, column, cell, event) {
        this.rowIndex = '-1'
        this.hoverOrderArr = [];
      }
    }
  }
</script>