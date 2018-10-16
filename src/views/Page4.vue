<template>
    <div>

        <el-form>
            <el-form-item label="昵称">
                <el-input v-model="queryCondition.similarNickName"></el-input>
            </el-form-item>
            <el-form-item label="流水号">
                <el-input v-model="queryCondition.sellerCode"></el-input>
            </el-form-item>
            <el-form-item label="余额">
                <el-input-number v-model="queryCondition.minMemberBalance"></el-input-number>
                －－
                <el-input-number v-model="queryCondition.maxMemberBalance"></el-input-number>
            </el-form-item>
            <el-form-item>
                <el-button type="primary" icon="el-icon-edit" @click="queryByCondition">查询</el-button>
                <el-button type="warning" icon="el-icon-delete" @click="resetCondition">重置</el-button>
            </el-form-item>
        </el-form>
        <el-table :data="datas">
            <el-table-column prop="id" label="SellerID"></el-table-column>
            <el-table-column prop="sellerCode" label="流水号"></el-table-column>
            <el-table-column prop="member.balance" label="余额"></el-table-column>
            <el-table-column prop="member.nickName" label="昵称"></el-table-column>
            <el-table-column prop="createDate" label="注册时间"></el-table-column>
        </el-table>
    </div>

</template>

<script>
    export default {
        name: "Page4",
        mounted: function () {
            this.query();
        },


        data: function () {
            return {
                queryCondition: {
                    sellerCode: "",
                    similarNickName: "",
                    maxMemberBalance: null,
                    minMemberBalance: 0,
                    pageNum: 0,
                    pageSize: 3,



                },
                datas: [],
                seller: {

                    id: 2,
                    sellerCode: "Seller_827672",
                    member: {
                        balance: 1496,
                        nickName: "周_38"
                    },
                    createDate: "2018-10-17",
                }

            }
        },
        methods: {
            query: function () {
                this.$http({
                    baseURL: 'http://localhost:8899/',
                    url: '/sellers',
                    method: 'post',
                    data: this.queryCondition,
                }).then(result => {
                    this.datas = result.data.content;
                }).catch(console.log);
            },
            queryByCondition:function () {

                this.$message.warning(JSON.stringify(this.queryCondition));
                this.query();
            }
        }
    }
</script>

<style scoped>

</style>
