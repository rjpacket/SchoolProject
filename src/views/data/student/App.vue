<template>
    <div id="app">

        <div class="page-title">会中往届学生信息征集</div>

        <div class="panel">
            *姓名：
            <div class="input-wrap">
                <x-input placeholder="请输入姓名" v-model="name"></x-input>
            </div>
        </div>

        <div class="panel">
            *性别：
            <div class="input-wrap">
                <x-input placeholder="请输入性别" v-model="sex"></x-input>
            </div>
        </div>

        <div class="panel">
            *届别：
            <div class="input-wrap">
                <x-input placeholder="请输入届别" v-model="year"></x-input>
            </div>
        </div>

        <div class="panel">
            *工作单位：
            <div class="input-wrap">
                <x-input placeholder="请输入工作单位" v-model="company"></x-input>
            </div>
        </div>

        <div class="panel">
            *职务：
            <div class="input-wrap">
                <x-input placeholder="请输入职务" v-model="job"></x-input>
            </div>
        </div>

        <div class="panel">
            *联系电话：
            <div class="input-wrap">
                <x-input placeholder="请输入联系电话" v-model="phone"></x-input>
            </div>
        </div>

        <div class="panel">
            *邮箱：
            <div class="input-wrap">
                <x-input placeholder="请输入邮箱" v-model="email"></x-input>
            </div>
        </div>

        <div class="panel">
            备注：
            <div class="input-wrap">
                <x-input placeholder="请输入备注" v-model="other"></x-input>
            </div>
        </div>

        <div class="btn-confirm">
            <x-button type="primary" v-on:click.native="clickConfirm">提交</x-button>
        </div>

        <div>
            <alert v-model="showAlert" title="提示" :content="content"></alert>
        </div>
    </div>
</template>

<script>

    import Lib from 'assets/js/Lib';

    import {Divider, XInput, XButton, Alert} from 'vux'

    export default {
        data() {
            return {
                name: '',
                sex: '',
                year: '',
                company: '',
                job: '',
                phone: '',
                email: '',
                other: '',
                showAlert: false,
                content: '暂不支持录入'
            }
        },
        components: {
            XInput,
            Divider,
            XButton,
            Alert
        },
        //实例初始化最之前，无法获取到data里的数据
        beforeCreate(){


        },
        //在挂载开始之前被调用
        beforeMount(){


        },
        //已成功挂载，相当ready()
        mounted(){


        },
        //相关操作事件
        methods: {
            clickConfirm () {
                let that = this;
                Lib.M.ajax({
                    'url':'http://47.96.127.217/api/v1/student',
                    'type': 'post',
                    'data': {
                      name: this.name,
                      sex: this.sex,
                      year: this.year,
                      company: this.company,
                      job: this.job,
                      phone: this.phone,
                      email: this.email,
                      other: this.other
                    },
                    'success':function (data){
                        if(data.code === 1){
                            that.content = '添加数据成功';
                            that.showAlert = true;
                        }else {
                            that.content = data.msg;
                            that.showAlert = true;
                        }
                    },
                    'error': function (error) {
                        that.content = '数据添加异常';
                        that.showAlert = true;
                    }
                });
            }
        }
    }
</script>

<style lang="less">
    .page-title{
        font-size: 2rem;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
    }

    .btn-confirm {
        margin-left: 1rem;
        margin-right: 1rem;
        margin-bottom: 2rem;
    }

    .panel {
        margin: 1rem;
    }

    .input-wrap {
        border: 1px solid #e4e4e4;
        border-radius: .5rem;
    }
</style>
