/**
* Created by zhangxin on 2017/3/1.
*/
<template>
    <div class="modal fade" id="userInfo" tabindex="-1" role="dialog" aria-labelledby="userInfoLabel" aria-hidden="true">
        <div class="modal-dialog modal-lg">
            <div class="modal-content">
                <div class="modal-header">
                    <button type="button" class="close" data-dismiss="modal" aria-hidden="true">&times;</button>
                    <h4 class="modal-title" id="userInfoLabel">用户详情</h4>
                </div>
                <div class="modal-body">
                    <div class="form-horizontal">
                        <div class="form-group">
                            <label class="control-label col-md-3">姓名：</label>
                            <div class="col-md-3">
                                <p class="form-control-static">{{userInfo.result.name}}</p>
                            </div>
                            <label class="control-label col-md-3">所属行业：</label>
                            <div class="col-md-3">
                                <p class="form-control-static">{{userInfo.result.trade}}</p>
                            </div>
                        </div>
                        <div class="form-group">
                            <label class="control-label col-md-3">所在地区：</label>
                            <div class="col-md-3">
                                <p class="form-control-static">{{userInfo.result.province}}-{{userInfo.result.city}}-{{userInfo.result.county}}</p>
                            </div>
                            <label class="control-label col-md-3">手机号：</label>
                            <div class="col-md-3">
                                <p class="form-control-static">{{userInfo.result.phone}}</p>
                            </div>
                        </div>
                        <div class="form-group">
                            <label class="control-label col-md-3">公司名称：</label>
                            <div class="col-md-3">
                                <p class="form-control-static">{{userInfo.result.company}}</p>
                            </div>
                            <label class="control-label col-md-3">用户状态：</label>
                            <div class="col-md-3">
                                <p class="form-control-static">{{userInfo.result.userStatus}}</p>
                            </div>
                        </div>
                        <div class="form-group">
                            <label class="control-label col-md-3">注册时间：</label>
                            <div class="col-md-3">
                                <p class="form-control-static">{{userInfo.result.registerDate}}</p>
                            </div>
                        </div>
                        <div class="form-group">
                            <label class="control-label col-md-3">套餐信息：</label>
                            <div class="col-md-9">
                                <p class="form-control-static">{{userInfo.result.packageName}}</p>
                            </div>
                        </div>
                        <div class="form-group">
                            <label class="control-label col-md-3">关键词配置：</label>
                            <div class="col-md-9">
                                <p class="form-control-static">{{userInfo.result.keywordList}}</p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<style scoped>
</style>
<script>
     /*
    * import '../../assets/vendor/iCkeck-v1.0.2/js/icheck.min';
    * import "vue-style-loader!css-loader!sass-loader!../../assets/vendor/iCkeck-v1.0.2/css/skins/square/blue.css";
    * import loginButton from './components/loginButton.vue';
    */
    export default{
        data(){
            return {
                userInfo:{
                    url:"../apis/user/findUserById",
                    params:"",
                    result:{}
                }
            }
        },
        components:{} ,
        methods:{
            post(urls, params, successFun, errorFun){
                this.$http.post(urls, params).then((response) => {
                    if (response.ok) {
                        successFun(response.data);
                    } else {
                        errorFun(response);
                    }
                });
            },
        },
        mounted(){
            let vm = this;
            $("#userInfo").on("shown.bs.modal",function () {
                vm.userInfo.params=vm.$store.state.userManager.userId;
                vm.post(vm.userInfo.url,vm.userInfo.params,function (response) {
                    if(response.success){
                        let obj =response.data;
                        obj.registerDate=new Date(response.data.registerDate).Format("yyyy-MM-dd hh:mm:ss");
                        vm.userInfo.result=obj;
                    }
                },function (error) {

                });
            })
        }
    }
</script>