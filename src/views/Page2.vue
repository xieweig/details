<template>
    <div class="home">
        <img alt="Vue logo" src="../assets/logo.png">
        <!--      title="ViewToModel界面（录入/修改）-->
        <el-form ref="personForm" :model="person" label-width="40px" :rules="personRules">
            <el-form-item label="姓名String" prop="name">
                <el-input v-model="person.name"></el-input>
            </el-form-item>
            <el-form-item label="年龄Number" prop="age">
                <el-input-number v-model="person.age"></el-input-number>
            </el-form-item>

            <el-form-item label="性别EnumString">
                <el-radio-group v-model="person.sex">
                    <el-radio v-for="i in sexEnum" :key="i" :label="i"></el-radio>
                </el-radio-group>
            </el-form-item>

            <el-form-item label="婚否Boolean">
                <el-switch v-model="person.married"
                active-text="右边为ｔｒｕｅ：已婚" inactive-text="左边：未婚"></el-switch>
            </el-form-item>

            <el-form-item label="出生日期Date">
                <el-date-picker type="date"
                                v-model="person.birthday" value-format="yyyy => MM => dd"
                                placeholder="birthday: " format="yyyy->MM->dd"></el-date-picker>
            </el-form-item>
            <el-form-item label="家庭住址 省 EnumString">
                <el-select v-model="person.homeAddress.province">
                    <el-option v-for="i in provinceEnum"
                               :value="i.value" :key="i.value" :label="i.label"></el-option>
                </el-select>
            </el-form-item>
            <el-form-item label="家庭住址 市 List<EnumString>">
                <el-checkbox-group v-model="person.homeAddress.city">
                    <el-checkbox v-for="i in cityEnum" :value="i" :key="i" :label="i"></el-checkbox>
                </el-checkbox-group>
            </el-form-item>
            <el-form-item>
                <el-button type="primary" @click="submit('personForm')" icon="el-icon-success">保存save</el-button>
                <el-button type="danger" @click="reset('personForm')" icon="el-icon-delete">重置reset</el-button>
            </el-form-item>
        </el-form>


        <el-form v-model="person" ref="showPerson">
            <el-form-item label="姓名String">
                <el-button type="info">{{person.name}}</el-button>
            </el-form-item>
            <el-form-item label="年龄Number">
                <el-button type="warning">{{person.age}}</el-button>
            </el-form-item>

            <el-form-item label="性别EnumString">
                <el-button type="success" round>{{person.sex}}</el-button>
            </el-form-item>

            <el-form-item label="婚否Boolean">
                <el-button type="danger" circle>{{person.married}}</el-button>
            </el-form-item>

            <el-form-item label="出生日期Date">
                <el-button type="primary" icon="el-icon-edit">{{person.birthday}}</el-button>
            </el-form-item>
            <el-form-item label="家庭住址">
                <el-row>
                    <el-col :span="8">{{person.homeAddress.province}}</el-col>
                    <el-col :span="2">省</el-col>
                    <el-col :span="8">{{person.homeAddress.city}}</el-col>
                    <el-col :span="2">市</el-col>
                </el-row>
                <el-row>
                    <!--注意 这里写的js代码量就太多了 不合适，所以有一种函数叫计算函数用来盛放此处的代码-->
<!--                    <el-col :span="8">{{provinceEnum
                        .filter(o=>o.value===person.homeAddress.province)
                        .map(o=>o.label)[0]}}-->
                        <el-col :span="8">{{provinceEnum
                            .find(o => o.value === person.homeAddress.province).label}}
                    </el-col>
                    <el-col :span="2">省</el-col>
                    <el-col :span="8">{{homeAddressEx}}</el-col>
                    <el-col :span="2">市</el-col>
                </el-row>
            </el-form-item>
            <el-form-item>
                <el-button type="primary" icon="el-icon-info" @click="getOne">模拟从后台获取一个</el-button>
            </el-form-item>
            <el-form-item>
                <el-button type="primary" icon="el-icon-info" @click="articleGetOne">getArticle</el-button>
            </el-form-item>
            <el-form-item>
                <el-button type="primary" icon="el-icon-info" @click="articlePublish">publishArticle</el-button>
            </el-form-item>
        </el-form>

    </div>
</template>

<script>
    export default {
        created:function(){
            this.provinceEnum=[{
                label: '山东',
                value: 'shan_dong'
            }, {
                label: '浙江',
                value: 'zhe_jiang'
            }, {
                label: '江苏',
                value: 'jiang_su'
            }];
        },
        mounted:function () {
            this.cityEnum = ['jinan', 'yantai', 'qingdao'];
            this.cityEnumEx=[{
                label: '英魂济南',
                value: 'jinan'
            }, {
                label: '霸气烟台',
                value: 'yantai'
            },{
                label:'威武青岛',
                value:'qingdao'
            }];
        },
        data() {
            return {
                sexEnum: ['boy', 'girl', 'unclear'],
                //java 中枚举也可以设置成map映射形式，但是一般后天不注重展示，数据库中一般用字母字符串记录，这样程序员能看懂
                // ，不会用数字和汉字，数字很难直观明白（但是可以加减计算排序），汉字有字符串编码问题。前台展示则要充分为用户考虑
                provinceEnum: [],
                cityEnum: [],
                cityEnumEx:[],

                //对应的后台是实体类 或者query_dto
                person: {
                    name: 'yu_er',
                    age: 10,
                    married: false,
                    sex: 'unclear',
                    birthday: '2018 => 06 => 06',
                    homeAddress: {
                        province: 'zhe_jiang',
                        city: ['qingdao', 'jinan'],
                    }
                },
                personRules: {
                    name: [
                        {required: true, message: '请输入name', trigger: 'blur'},
                        {min: 3, max: 5, message: '长度在 3 到 5 个字符', trigger: 'blur'}
                    ],
                    age: [
                        {required: true, message: '请选择age', trigger: 'change'}
                    ],
                }


            }
        },
        computed: {
            homeAddressEx:function () {
                       return this.person.homeAddress.city
                           .map(i => this.cityEnumEx
                               .find(o=> o.value === i).label)
                           .join("==")
                    //return this .person.homeAddress.city.join("==")

            },

        },
        methods: {
            /*箭头函数与其上下文代码共享相同的词法this*/
            submit: function (formName) {
                this.$refs[formName].validate((valid)=>{
                    if (valid){
                        this.$message.success("待存储的对象 " + JSON.stringify(this.person));
                        return null;
                    }
                    this.$message.warning("待存储对象不符合格式要求");

                });
            },
            reset: function (formName) {
                this.$refs[formName].resetFields();
            },
            getOne: function () {

                let person1 = {
                    name: 'nan_gua',
                    age: 40,
                    married: true,
                    sex: 'boy',
                    birthday: '1999 => 06 => 06',
                    homeAddress: {
                        province: 'shan_dong',
                        city: ['qingdao',],
                    }
                };
                this.person = person1;
            },
            articleGetOne:function(){
                this.$http({
                        baseURL:"http://127.0.0.1:8899/",
                        url:"/seller/Seller_537141",
                        method:"get",

                    }
                ).then(({data}) => this.$message.success(JSON.stringify(data)))
                    .catch(console.log)
            },

            articlePublish:function () {
                var dataS = {
                    "articleCode": "",
                    "articleType": "food",
                    "id": 0,
                    "price": 55,
                    "seller": {
                        "id": 12,
                        "member": {
                            "balance": 0,
                            "nickName": "string"
                        },
                        "sellerCode": "Seller_537141"
                    }
                };

                this.$http({
                    baseURL:"http://127.0.0.1:8899/",
                    url:"/article",
                    method:"put",
                    data:dataS
                    }
                ).then(({data}) => this.$message.success(JSON.stringify(data)))
                    .catch(console.log)
            }
        }
    }
</script>

<style scoped>

</style>
