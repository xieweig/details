<template>
    <div>
        <el-row>
            <el-col :span="6">

        <h5>下拉菜单示例</h5>
        <el-menu class="el-menu"
                 background-color="#202020" text-color="#fff" active-text-color="#aaa"
                 :default-active="$router.path" router>
            <el-menu-item index="/second">form</el-menu-item>
            <el-submenu index="/hr">
                <div slot="title">
                    <i class="el-icon-check"></i>人力资源系统
                </div>

                    <el-menu-item index="/offer">入职流程</el-menu-item>
                    <el-menu-item index="/salary">月薪结算</el-menu-item>
                    <el-menu-item index="/campus">校园招聘会</el-menu-item>

            </el-submenu>
            <el-submenu index="/erp">
                <div slot="title">
                    <i class="el-icon-location-outline"></i>进销存系统
                </div>
                    <el-menu-item index="/income">进货流程</el-menu-item>
                    <el-menu-item index="/delivery">配送流程</el-menu-item>
                    <el-menu-item index="/store">仓库存货</el-menu-item>
                    <el-menu-item index="/balance">平账流程</el-menu-item>
            </el-submenu>
            <el-submenu index="/act">
                <div slot="title">
                    <i class="el-icon-location"></i>活动业务系统
                </div>
                <el-menu-item index="/basic">活动基本信息</el-menu-item>
                <el-menu-item index="/summary">总结报告</el-menu-item>
            </el-submenu>
        </el-menu>

            </el-col>
            <el-col :span="18"></el-col>
        </el-row>
    </div>
</template>

<script>
    export default {

    }
</script>

<style scoped>

</style>
