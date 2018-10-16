<template>
    <div>
        <el-button type="success" icon="el-icon-edit" @click="getAll">select * from person</el-button>
        <el-table :data="persons"  height="200px"  stripe="true" highlight-current-row="true">

            <el-table-column prop="basic.name"
                             label="姓名" width="200px"></el-table-column>
            <el-table-column prop="basic.age"
                             label="年龄" width="150px"></el-table-column>
            <el-table-column prop="basic.sex"
                             label="性别" width="150px"></el-table-column>
            <el-table-column prop="role.studentCode"
                             label="学号" width="200px"></el-table-column>
            <el-table-column prop="role.grade"
                             label="班级" width="150px"></el-table-column>
            <el-table-column prop="role.major"
                             label="主修技能" width="100px"></el-table-column>
            <el-table-column label="AGE" width="80px">
                <template slot-scope="scope">

                    <i class="el-icon-time"></i>
                    <span style="margin-left: 10px">{{ scope.row.basic.age+1 }}</span>
                </template>

            </el-table-column>
            <!-- <el-table-column prop="role.majorEx(role.major)"
                              label="好看的主修技能"></el-table-column>-->
            <el-table-column label="好看的主修技能" width="250px" fixed="left">
                <template slot-scope="personsView">
                    <el-button-group>
                        <el-button type="warning" icon="el-icon-edit"
                                   @click="update(personsView.$index,personsView.row)">
                            {{personsView.row.basic.name}}
                        </el-button>
                        <el-button type="danger" icon="el-icon-delete">
                            {{personsView.row.basic.name}}
                        </el-button>
                    </el-button-group>
                </template>
            </el-table-column>
            <el-table-column label="see Major" width="200px">
                <template slot-scope="scope">
                    <el-select v-model="scope.row.role.major">
                        <el-option v-for="item in majors"
                                   :label="item.label" :value="item.value" :key="item.value"></el-option>
                    </el-select>
                </template>
            </el-table-column>
            <el-table-column label="Major Map" width="200px">
                <template slot-scope="scope">
                    <span>{{majorEx(scope.row.role.major)}}</span>
                </template>
            </el-table-column>

        </el-table>

        <el-table :data="persons">
            <el-table-column property="basic.name"
                             label="姓名" width="200px"></el-table-column>
            <el-table-column property="basic.age"
                             label="年龄" width="50px"></el-table-column>
            <el-table-column property="basic.sex"
                             label="性别"></el-table-column>
            <el-table-column label="编辑">
                <template slot-scope="scope">
                    <el-button-group>
                        <el-button type="primary" circle="true" icon="el-icon-edit"
                        @click="openDialog(scope.row)">详细信息</el-button>
                        <el-button type="danger" circle="true" icon="el-icon-delete"
                        @click="update(scope.$index,scope.row)">删除条目</el-button>

                        <el-dialog :visible.sync="dialogKey" class="el-dialog">
                            <el-form>

                                <el-form-item label="姓名" >
                                    <el-input v-model="person.basic.name"></el-input>
                                </el-form-item>
                                <el-form-item label="AGE">
                                    <el-input-number v-model="person.basic.age"></el-input-number>
                                </el-form-item>
                            </el-form>
                            <template slot="footer" class="el-dialog__footer">
                                <el-button-group>
                                    <el-button type="warning" round="true"
                                               @click="dialogKey = false">取消</el-button>
                                    <el-button type="primary" round="true"
                                               @click="updates">保存</el-button>
                                </el-button-group>
                            </template>
                        </el-dialog>

                    </el-button-group>
                </template>
            </el-table-column>
        </el-table>
        <community></community>

    </div>
</template>

<script>
    import community from '@/components/Community.vue'

    export default {
        components:{
            community
        },

        data: function () {
            const sexes = [{
                label: '男',
                value: 'boy'
            }, {
                label: '女',
                value: 'girl'
            }];

            const majors = [{
                label: 'SpringBoot2',
                value: 'jdk8'
            }, {
                label: 'Vue2',
                value: 'es6'
            }, {
                label: 'TensorFlow',
                value: 'py3'
            }];

            const grades = ['2015', '2016', '2017', '2018'];

            return {
                person: {
                    basic: {
                        name: 'aaa',
                        age: 0,
                        sex: 'man'
                    },
                    role: {
                        studentCode: '',
                        major: '',
                        grade: ''
                    }


                },
                persons: [],
                majors: majors,
                sexes: sexes,
                grades: grades,

                dialogKey:false,

            }
        },
        methods: {
            update: function (index, row) {
                this.$message.warning(index+" ___ "+JSON.stringify(row))
            },
            openDialog:function(row){
                this.dialogKey=true;
                this.person = row;

            },
            updates: function (row) {

                this.$message.warning("发送请求 ___ 并返回更新后的table内容 "+JSON.stringify(row));
                this.dialogKey=false
            },
            getAll: function () {
                //此处模拟一个请求假设返回值如下
                var results = [{
                    basic: {
                        name: '蔡文姬',
                        age: 20,
                        sex: 'girl'
                    },
                    role: {
                        studentCode: '0203008',
                        major: 'es6',
                        grade: '2016'
                    }
                }, {
                    basic: {
                        name: '张衡',
                        age: 30,
                        sex: 'boy'
                    },
                    role: {
                        studentCode: '0203007',
                        major: 'jdk8',
                        grade: '2018'
                    }
                }, {
                    basic: {
                        name: '陆游',
                        age: 60,
                        sex: 'boy'
                    },
                    role: {
                        studentCode: '0203018',
                        major: 'py3',
                        grade: '2017'
                    }
                }];
                this.persons = results;
            },
            majorEx: function (major) {
                return this.majors.filter(o => o.value === major)
                    .map(o => o.label)[0];
            }
        },
        computed: {
            majorC: function () {
                return this.majors.filter(o => o.value === this.person.role.major)
                    .map(o => o.label)[0];
            }


        },


    }
</script>

<style scoped>

</style>
