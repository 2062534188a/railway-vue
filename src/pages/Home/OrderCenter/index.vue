<template>
  <el-container>
    <el-main
      ><el-card class="box-card">
        <div slot="header" class="clearfix">
          <span>我的订单</span>
          <el-button style="float: right; padding: 3px 0" type="text"
            >刷新</el-button
          >
        </div>

        <div class="text item">
          <el-form
            :model="ruleForm"
            status-icon
            ref="ruleForm"
            :inline="true"
            class="demo-ruleForm"
            size="mini"
          >
            <el-form-item label="订单号" prop="orderSn">
              <el-input
                type="text"
                v-model="ruleForm.orderSn"
                autocomplete="off"
              ></el-input>
            </el-form-item>
            <el-form-item label="订单状态" prop="orderStatus">
              <el-input
                type="text"
                v-model="ruleForm.orderStatus"
                autocomplete="off"
              ></el-input>
            </el-form-item>

            <el-form-item>
              <el-button type="primary" @click="submitForm('ruleForm')"
                >提交</el-button
              >
              <el-button @click="resetForm('ruleForm')">重置</el-button>
            </el-form-item>
          </el-form>
          <el-table :data="tableData" style="width: 100%">
            <el-table-column type="expand">
              <template slot-scope="props">
                <el-form label-position="left" inline class="demo-table-expand">
                  <el-form-item label="订单号">
                    <span>{{ props.row.orderSn }}</span>
                  </el-form-item>
                  <el-form-item label="订单金额">
                    <span>{{ props.row.orderPrice }}</span>
                  </el-form-item>
                  <el-form-item label="真实姓名">
                    <span>{{ props.row.userIdName }}</span>
                  </el-form-item>
                  <el-form-item label="手机号">
                    <span>{{ props.row.userPhone }}</span>
                  </el-form-item>
                  <el-form-item label="下单时间">
                    <span>{{ props.row.createTime }}</span>
                  </el-form-item>
                  <el-form-item label="结束时间">
                    <span>{{ props.row.closeTime }}</span>
                  </el-form-item>
                  <el-form-item label="订单状态">
                    <span>{{ props.row.orderStatus }}</span>
                  </el-form-item>
                </el-form>
              </template>
            </el-table-column>
            <el-table-column label="订单号" prop="orderSn"> </el-table-column>
            <el-table-column label="订单金额" prop="orderPrice">
            </el-table-column>
            <el-table-column label="创建时间" prop="createTime">
            </el-table-column>
            <el-table-column label="订单状态" prop="orderStatus">
            </el-table-column>
          </el-table>
        </div>
      </el-card>
    </el-main>
  </el-container>
</template>

<script>
import { queryMyOrder } from "@/api/api";
export default {
  name: "OrderCenter",
  data() {
    return {
      ruleForm: {
        orderSn: "",
        orderStatus: "",
      },
      tableData: [
        {
          order_sn: "12987122",
          order_price: "好滋好味鸡蛋仔",
          user_id_name: "江浙小吃、小吃零食",
          user_phone: "荷兰优质淡奶，奶香浓而不腻",
          create_time: "上海市普陀区真北路",
          close_time: "上海市普陀区真北路",
          order_status: "王小虎夫妻店",
        },
      ],
    };
  },
  methods: {
    onSubmit() {},
    resetForm(formName) {
      console.log(formName);
      this.$refs[formName].resetFields();
    },
    queryMyOrderData() {
      queryMyOrder()
        .then((res) => {
          const orderData = res.data;
          this.tableData = orderData;
          console.log(orderData);
        })
        .catch((err) => {});
    },
  },
  mounted() {
    this.queryMyOrderData();
  },
};
</script>

<style scoped>
.demo-table-expand {
  font-size: 0;
}
.demo-table-expand label {
  width: 90px;
  color: #99a9bf;
}
.demo-table-expand .el-form-item {
  margin-right: 0;
  margin-bottom: 0;
  width: 50%;
}
</style>
