<template>
    <el-form>
        <el-form-item label="社团名称">
            <el-input v-model="community.name"></el-input>
        </el-form-item>
        <el-form-item label="成立日期">
            <el-date-picker v-model="community.createTime" value-format="yyyy-MM-dd"></el-date-picker>
        </el-form-item>
        <el-form-item label="社团类型">
            <el-checkbox-group v-model="community.type">
                <el-checkbox v-for="i in types"
                             :key="i.value" :label="i.value">{{i.text}}</el-checkbox>
            </el-checkbox-group>
        </el-form-item>
        <el-form-item>
            <el-button type="warning" @click="debug(community)">保存</el-button>
        </el-form-item>
    </el-form>

</template>

<script>
    export default {
        data(){
            return{
                community:{
                    name:'动漫社',
                    createTime:'',
                    type:[],
                },
                types:[{
                    text:'二次元',
                    value:'aa007'
                },{
                    text:'韩国女团',
                    value:'bb008'
                },{
                    text:'非主流肥宅',
                    value:'cc009'
                }]

            }
        },
        methods:{
            debug:function (o) {
                this.$message.success("DEBUG: "+JSON.stringify(o));
            }
        }

    }
</script>

<style scoped>

</style>
