/**
* Created by zhangxin on 2017/3/1.
*/
<template>
    <div class="modal fade" id="updateUser" tabindex="-1" role="dialog" aria-labelledby="updateUserLabel" aria-hidden="true">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <button type="button" class="close" data-dismiss="modal" aria-hidden="true">&times;</button>
                    <h4 class="modal-title" id="updateUserLabel">修改用户</h4>
                </div>
                <div class="modal-body">
                    <div class="form-horizontal">
                        <div class="form-group">
                            <label class="control-label col-md-3">姓名：</label>
                            <div class="col-md-6">
                                <input type="text" class="form-control" placeholder="请输入姓名" v-model="addUser.params.name" />
                            </div>
                        </div>
                        <div class="form-group">
                            <label class="control-label col-md-3">手机：</label>
                            <div class="col-md-6">
                                <input type="text" class="form-control" placeholder="请输入手机" v-model="addUser.params.phone" />
                            </div>
                        </div>
                        <div class="form-group">
                            <label class="control-label col-md-3">公司名称：</label>
                            <div class="col-md-6">
                                <input type="text" class="form-control" placeholder="请输入公司名称" v-model="addUser.params.company" />
                            </div>
                        </div>
                        <div class="form-group">
                            <label class="control-label col-md-3">所在地区：</label>
                            <div class="col-md-3">
                                <select class="form-control selectpicker mcity shengs" v-model="searchCon.sheng1Val" id="sheng1" title="省">
                                    <option v-for="item in sheng1">{{item}}</option>
                                </select>
                            </div>
                            <div class="col-md-3">
                                <select class="form-control selectpicker mcity shis" v-model="searchCon.shi1Val" id="shi1" title="市">
                                    <option v-for="item in shi1">{{item}}</option>
                                </select>
                            </div>
                            <div class="col-md-3">
                                <select class="form-control selectpicker mcity xians" v-model="searchCon.xian1Val" id="xian1" title="县／区">
                                    <option v-for="item in xian1">{{item}}</option>
                                </select>
                            </div>
                            <div class="col-md-offset-3 col-md-3">
                                <label class="checkbox">
                                    <input type="checkbox" class="mbx" />
                                    不限地区
                                </label>
                            </div>
                        </div>
                        <div class="form-group">
                            <label class="col-md-3 control-label">所属行业：</label>
                            <div class="col-md-6">
                                <select class="form-control selectpicker trade" title="请选择所属行业" v-model="addUser.params.trade">
                                    <option value="">不限</option>
                                    <option v-for="item in userTrade1.result" v-bind:value="item.name">{{item.name}}</option>
                                </select>
                            </div>
                        </div>
                        <div class="form-group">
                            <label class="col-md-3 control-label">用户状态：</label>
                            <div class="col-md-6">
                                <label>
                                    <input type="radio" name="userStatus" value="试用" v-if="addUser.params.userStatus=='试用'" checked />
                                    <input type="radio" name="userStatus" value="试用" v-else />
                                    试用
                                </label>
                                <label>
                                    <input type="radio" name="userStatus" value="正式" v-if="addUser.params.userStatus=='正式'" checked />
                                    <input type="radio" name="userStatus" value="正式" v-else />
                                    正式
                                </label>
                                <label>
                                    <input type="radio" name="userStatus" value="冻结" v-if="addUser.params.userStatus=='冻结'" checked />
                                    <input type="radio" name="userStatus" value="冻结" v-else />
                                    冻结
                                </label>
                            </div>
                        </div>
                        <div class="form-group">
                            <label class="col-md-3 control-label">套餐状态：</label>
                            <div class="col-md-9">
                                <label>
                                    <input type="radio" value="" name="packageId" v-if="addUser.params.packageId=='' || addUser.params.packageId==null || addUser.params.packageId==undefined" checked/>
                                    <input type="radio" value="" name="packageId" v-else-if="addUser.params.packageId!='' || addUser.params.packageId!=null || addUser.params.packageId!=undefined" />
                                    未办理套餐
                                </label>
                                <label v-for="item in packageList1.result">
                                    <input type="radio" v-bind:value="item.id" v-if="item.id==addUser.params.packageId" checked name="packageId"/>
                                    <input type="radio" v-bind:value="item.id" v-else name="packageId"/>
                                    {{item.name}}
                                </label>
                            </div>
                        </div>
                        <div class="form-group">
                            <label class="col-md-3 control-label">关键词配置：</label>
                            <div class="col-md-6">
                                <textarea class="form-control" placeholder="请输入您需要添加的关键词，批量添加关键词请使用中文逗号隔开" v-model="addUser.params.keywordList"></textarea>
                            </div>
                            <!--<div class="col-md-offset-3 col-md-6">-->
                            <!--<div class="upload-box">-->
                            <!--<a href="javascript:void(0);"><img src="./images/set_icon.png"/>批量添加</a>-->
                            <!--<a href="javascript:void(0);"><img src="./images/set_icon1.png" />下载文件模版</a>-->
                            <!--</div>-->
                            <!--</div>-->
                        </div>
                    </div>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-default" data-dismiss="modal">&nbsp;&nbsp; 取 消 &nbsp;&nbsp;</button>
                    <button type="button" class="btn btn-em" @click="addUsers()">&nbsp;&nbsp; 提 交 &nbsp;&nbsp;</button>
                </div>
            </div>
        </div>
    </div>
</template>
<style scoped lang="scss">
    .modal{
    .modal-content{
        border-radius: 0;
    .modal-body{
    textarea{
        height:150px;
        border-radius: 5px 5px 0 0;
        resize: none;
    }
    .upload-box{
        background-color: #f2f2f2;
        border-radius: 0 0 5px 5px;
        border:1px solid #ccc;
        border-top:none;
    a{
        margin-left: 0.4%;
        display: inline-block;
        width: 48%;
        color: #999999;
        padding-top: 10px;
        padding-bottom: 10px;
        text-align: center;
        font-weight: 400;
        background-color: #f2f2f2;
        vertical-align: middle;
        text-decoration:none;
    &:first-child{
         border-right:1px solid #ccc;
    img{
        margin-right: 5px;
    }
    }
    }
    }
    label{
        font-weight: 400;
    }
    }
    }
    .modal-footer{
        border-top:none;
        text-align: center;
    }
    }
</style>
<script>
    import data from '../../../assets/data/data';
    export default{
        data(){
            return{
                "msg":"添加用户",
                getUser:{
                    url:"../apis/user/findUserById",
                },
                addUser:{
                    url:"../apis/user/saveUser",
                    params:{}
                },
                packageList1:{
                    url:"../apis/package/findOnShelvesList",
                    result:{}
                },
                userTrade1:{
                    url:"../apis/personal/findAllTrade",
                    result:{}
                },
                searchData:data,
                sheng1:data.citySearch.GP,
                shi1:data.citySearch.GT[0],
                xian1:data.citySearch.GC[0][0],
                searchCon:{
                    sheng1Val:"",
                    shi1Val:"",
                    xian1Val:"",
                },
            }
        },
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
            addUsers(){
                let vm =this;
                vm.addUser.params.province=vm.searchCon.sheng1Val;
                vm.addUser.params.city=vm.searchCon.shi1Val;
                vm.addUser.params.county=vm.searchCon.xian1Val;
                vm.post(vm.addUser.url,vm.addUser.params,function(response){
                    if(response.success){
                        $("#updateUser").modal("hide");
                        vm.$router.push({path:"/home/success"});
                    }else{
                        alert(response.message);
                    }
                },function (error) {
                    console.log(error)
                });
            }
        },
        mounted(){
            let vm=this,shiIndex1,xianIndex1,trade,province='北京',city='北京',county='东城区';
            $("#updateUser").on("show.bs.modal",function () {
                vm.post(vm.getUser.url,vm.$store.state.userManager.userId, function (response) {
                    if (response.success) {
                        vm.addUser.params = response.data;
                        trade=response.data.trade;
                        province=vm.addUser.params.province;
                        city=vm.addUser.params.city;
                        county=vm.addUser.params.county;
                        vm.post(vm.packageList1.url, "", function (response) {
                            if (response.success) {
                                if (response.data.length > 0) {
                                    vm.packageList1.result = response.data;
                                    setTimeout(function () {
                                        $(".mbx").iCheck({
                                            checkboxClass : 'icheckbox_square-blue',
                                        }).on("ifChecked",function(){
                                            vm.searchCon.sheng1Val="",
                                                vm.searchCon.shi1Val="",
                                                vm.searchCon.xian1Val="",
                                                $(".mcity").selectpicker('hide').selectpicker('val','').selectpicker('refresh');
                                        }).on("ifUnchecked",function () {
                                            $(".mcity").selectpicker('show').selectpicker('val','').selectpicker('refresh');
                                        });
                                        $("input[name=userStatus]").iCheck({
                                            radioClass : 'iradio_square-blue',
                                        }).on("ifChecked",function () {
                                            vm.addUser.params.userStatus=$(this).val();
                                        });
                                        $("input[name=packageId]").iCheck({
                                            radioClass : 'iradio_square-blue',
                                        }).on("ifChecked",function () {
                                            vm.addUser.params.packageId=$(this).val();
                                        });
                                    },300);
                                }
                            }
                        }, function (error) {
                            console.log(error);
                        });
                    }
                }, function (error) {
                    console.log(error);
                });
            }).on("shown.bs.modal",function () {
                shiIndex1=vm.searchData.citySearch.GP.indexOf(province);
                vm.shi1=vm.searchData.citySearch.GT[shiIndex1];
                xianIndex1=vm.searchData.citySearch.GT[shiIndex1].indexOf(city);
                vm.xian1=vm.searchData.citySearch.GC[shiIndex1][xianIndex1];
                vm.post(vm.userTrade1.url, "", function (response) {
                    if (response.success) {
                        if (response.data.length > 0) {
                            vm.userTrade1.result = response.data;
                            $(".shengs").selectpicker('val',province).selectpicker("refresh");
                            $(".shis").selectpicker('val',city).selectpicker("refresh");
                            $(".xians").selectpicker('val',county).selectpicker("refresh");
                            setTimeout(()=>{
                                vm.addUser.params.trade=trade;
                                $(".trade").selectpicker("refresh").selectpicker('val',trade);
                            },200);
                        }
                    }
                }, function (error) {
                    console.log(error);
                });
            }).on("hidden.bs.modal",function () {
                vm.addUser.params={};
                vm.packageList1.result={};
                vm.userTrade1.result={};
            });
            $("#sheng1").on("changed.bs.select",function (e,clickedIndex) {
                shiIndex1=clickedIndex-1;
                vm.shi1=vm.searchData.citySearch.GT[shiIndex1];
            }).on("hide.bs.select",function () {
                $("#shi1").selectpicker("refresh").selectpicker('val', '');
                $("#xian1").selectpicker("refresh").selectpicker('val', '');
            });
            $("#shi1").on("changed.bs.select",function (e,clickedIndex) {
                xianIndex1=clickedIndex-1;
                vm.xian1=vm.searchData.citySearch.GC[shiIndex1][xianIndex1];
            }).on("hide.bs.select",function () {
                $("#xian1").selectpicker("refresh").selectpicker('val', '');
            });
        }
    }
</script>