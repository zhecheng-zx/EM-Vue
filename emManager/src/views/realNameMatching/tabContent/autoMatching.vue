/**
* Created by zhangxin on 2017/2/24.
*/
<template>
    <div id="autoMatching">
        <p class="text-right">
            今天<span class="text-em">{{matchingNumber.number}}</span>条实名匹配
        </p>
        <div class="people-info">
            <div class="photo">
                <img src="./images/photo.png" alt="头像" />
            </div>
            <p class="text-center">{{receiveMatchingTask.result.author}}</p>
            <p class="text-center">
                <label>线索来源：</label>
                <span>{{receiveMatchingTask.result.source}}</span>
                <label>线索发布时间：</label>
                <span>{{receiveMatchingTask.result.publishDate}}</span>
            </p>
            <p class="text-center">
                <a :href="receiveMatchingTask.result.homeLink" target="_blank" class="btn btn-default">发布者主页</a>
                <a href="javascript:void(0);" class="btn btn-default">复制发布者主页链接</a>
                <a :href="receiveMatchingTask.result.link" target="_blank" class="btn btn-default">原文链接</a>
            </p>
            <div class="form-box">
                <div class="form-horizontal">
                    <div class="form-group">
                        <labeL class="col-md-4 control-label">真实姓名：</labeL>
                        <div class="col-md-4">
                            <input class="form-control" type="text" v-model="saveMatching.params.realname" placeholder="请您输入真实姓名" />
                        </div>
                    </div>
                    <div class="form-group">
                        <labeL class="col-md-4 control-label nopadding">性别：</labeL>
                        <div class="col-md-4">
                            <label>
                                <input class="form-control" type="radio" v-model="saveMatching.params.sex" name="sex" value="男" />
                                男
                            </label>
                            <label>
                                <input class="form-control" type="radio" v-model="saveMatching.params.sex" name="sex" value="女" />
                                女
                            </label>
                        </div>
                    </div>
                    <div class="form-group">
                        <labeL class="col-md-4 control-label">手机号：</labeL>
                        <div class="col-md-4">
                            <input class="form-control" type="text" v-model="saveMatching.params.phone" placeholder="请您输入手机号" />
                        </div>
                    </div>
                    <div class="form-group">
                        <labeL class="col-md-4 control-label">QQ：</labeL>
                        <div class="col-md-4">
                            <input class="form-control" type="text" v-model="saveMatching.params.qq" placeholder="请您输入QQ" />
                        </div>
                    </div>
                    <div class="form-group">
                        <labeL class="col-md-4 control-label">微信：</labeL>
                        <div class="col-md-4">
                            <input class="form-control" type="text" v-model="saveMatching.params.wechat" placeholder="请您输入微信" />
                        </div>
                    </div>
                    <div class="form-group">
                        <labeL class="col-md-4 control-label">邮箱：</labeL>
                        <div class="col-md-4">
                            <input class="form-control" type="text" v-model="saveMatching.params.email" placeholder="请您输入邮箱" />
                        </div>
                    </div>
                    <div class="form-group">
                        <labeL class="col-md-4 control-label">地址：</labeL>
                        <div class="col-md-2">
                            <select class="form-control selectpicker city" v-model="searchCon.shengVal" id="sheng" title="省">
                                <option v-for="item in sheng">{{item}}</option>
                            </select>
                        </div>
                        <div class="col-md-2">
                            <select class="form-control selectpicker city" v-model="searchCon.shiVal" id="shi" title="市">
                                <option v-for="item in shi">{{item}}</option>
                            </select>
                        </div>
                        <div class="col-md-2">
                            <select class="form-control selectpicker city" v-model="searchCon.xianVal" id="xian" title="县／区">
                                <option v-for="item in xian">{{item}}</option>
                            </select>
                        </div>
                    </div>
                    <div class="form-group">
                        <labeL class="col-md-4 control-label">其他信息：</labeL>
                        <div class="col-md-4">
                            <div class="input-textarea-group">
                                <input class="form-control" type="text" v-model="saveMatching.params.otherInfoName" placeholder="请您输入标题" />
                                <textarea class="form-control textarea" v-model="saveMatching.params.otherInfoContent" placeholder="请您输入信息内容">

                                </textarea>
                            </div>
                        </div>
                    </div>
                    <div class="form-group matching-btn-box">
                        <div class="col-md-4 col-md-offset-4 text-center">
                            <button class="btn btn-dark" type="button" @click="saveMathcingFalseFun()">无法匹配</button>
                            <button class="btn btn-em" type="button" @click="saveMathcingFun()">匹配完成</button>
                        </div>
                    </div>
                    <div class="form-group reMatching-btn-box hide">
                        <div class="col-md-4 col-md-offset-4 text-center">
                            <button class="btn btn-dark" type="button" @click="reSaveMathcingFalseFun()">无法匹配</button>
                            <button class="btn btn-em" type="button" @click="reSaveMathcingFun()">匹配完成</button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<style scoped lang="scss">
    .people-info{
        .photo{
            margin:0 auto 10px;
            width:85px;
            height:85px;
            line-height: 85px;
            text-align: center;
            border-radius: 50px;
            box-shadow: 0 0 10px rgba(0,0,0,.2);
        }
        p.text-center:nth-of-type(2){
            font-size:13px;
            label{font-weight: 400;}
            span{margin-right: 10px;color:#333333;}
        }
        p.text-center:nth-of-type(3){
            margin-bottom: 25px;
            .btn{margin-right: 15px;}
        }
    }
    p.text-right{margin-top: 25px;}
</style>
<script>
    /*
     * import '../../assets/vendor/iCkeck-v1.0.2/js/icheck.min';
     * import "vue-style-loader!css-loader!sass-loader!../../assets/vendor/iCkeck-v1.0.2/css/skins/square/blue.css";
     * import loginButton from './components/loginButton.vue';
     */
    import data from '../../../assets/data/data';
    export default{
        data(){
            return {
                searchData:data,
                sheng:data.citySearch.GP,
                shi:data.citySearch.GT[0],
                xian:data.citySearch.GC[0][0],
                searchCon:{
                    shengVal:"",
                    shiVal:"",
                    xianVal:"",
                },
                matchingNumber:{
                    url:"../../apis/judge/findMatchRecordCount",
                    params:"",
                    number:""
                },
                receiveMatchingTask:{
                    url:"../../apis/matching/receiveMatchingTask",
                    params:{
                        matchingSource:"自助匹配"
                    },
                    result:{}
                },
                saveMatching:{
                    url:"../../apis/matching/saveMatchingInfo",
                    params:{
                        salesLeadsId:"",
                        realname:"",
                        sex:"男",
                        phone:"",
                        qq:"",
                        wechat:"",
                        email:"",
                        address:"",
                        otherInfoName:"",
                        otherInfoContent:"",
                        updateUser:""
                    },
                    result:{}
                },
                getSalesLeads:{
                    url:"../../apis/matching/findMatchingDetails",
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
            /*领取自助匹配任务*/
            getList(){
                let vm =this,params={
                    salesLeadsId:"",
                    realname:"",
                    sex:"男",
                    phone:"",
                    qq:"",
                    wechat:"",
                    email:"",
                    address:"",
                    otherInfoName:"",
                    otherInfoContent:"",
                    updateUser:""
                },searchCon={
                    shengVal:"",
                    shiVal:"",
                    xianVal:"",
                };
                vm.receiveMatchingTask.result={};
                vm.saveMatching.params=params;
                vm.post(vm.receiveMatchingTask.url,vm.receiveMatchingTask.params,function (response) {
                    if(response.success){
                        let result=response.data;
                        result.publishDate=new Date(response.data.publishDate).Format("yyyy-MM-dd hh:mm:ss");
                        vm.receiveMatchingTask.result=result;
                        vm.getMatchingNumber();
                        setTimeout(()=>{
                            $('.city').selectpicker("val","").selectpicker("refresh");
                        },200);
                    }
                },function (error) {
                    console.log(error);
                });
            },
            /*匹配条数*/
            getMatchingNumber(){
                let vm =this;
                vm.post(vm.matchingNumber.url,vm.matchingNumber.params,function (response) {
                    if(response.success){
                        vm.matchingNumber.number=response.data;
                    }
                },function (error) {
                    console.log(error);
                });
            },
            saveMathcingFun(){
                let vm =this,address = vm.searchCon.shengVal+"-"+vm.searchCon.shiVal+"-"+vm.searchCon.xianVal;
                vm.saveMatching.params.salesLeadsId = vm.receiveMatchingTask.result.id;
                vm.saveMatching.params.address = address;
                vm.saveMatching.params.updateUser = sessionStorage.getItem("userAccount");
                vm.saveMatching.params.matchingResult = "匹配成功";
                vm.post(vm.saveMatching.url,vm.saveMatching.params,function (response) {
                    if(response.success){
                        vm.getList();
                    }
                },function (error) {
                    console.log(error);
                });
            },
            saveMathcingFalseFun(){
                let vm =this,address = vm.searchCon.shengVal+"-"+vm.searchCon.shiVal+"-"+vm.searchCon.xianVal;
                vm.saveMatching.params.salesLeadsId = vm.receiveMatchingTask.result.id;
                vm.saveMatching.params.address = address;
                vm.saveMatching.params.updateUser = sessionStorage.getItem("userAccount");
                vm.saveMatching.params.matchingResult = "暂未匹配";
                vm.post(vm.saveMatching.url,vm.saveMatching.params,function (response) {
                    if(response.success){
                        vm.getList();
                    }
                },function (error) {
                    console.log(error);
                });
            },
            reSaveMathcingFalseFun(){
                let vm =this,address = vm.searchCon.shengVal+"-"+vm.searchCon.shiVal+"-"+vm.searchCon.xianVal;
                vm.saveMatching.params.salesLeadsId = vm.receiveMatchingTask.result.id;
                vm.saveMatching.params.address = address;
                vm.saveMatching.params.updateUser = sessionStorage.getItem("userAccount");
                vm.saveMatching.params.matchingResult = "暂未匹配";
                vm.post(vm.saveMatching.url,vm.saveMatching.params,function (response) {
                    if(response.success){
                        vm.$emit("currentTab2");
                    }
                },function (error) {
                    console.log(error);
                });
            },
            reSaveMathcingFun(){
                let vm =this,address = vm.searchCon.shengVal+"-"+vm.searchCon.shiVal+"-"+vm.searchCon.xianVal;
                vm.saveMatching.params.salesLeadsId = vm.receiveMatchingTask.result.id;
                vm.saveMatching.params.address = address;
                vm.saveMatching.params.updateUser = sessionStorage.getItem("userAccount");
                vm.saveMatching.params.matchingResult = "匹配成功";
                vm.post(vm.saveMatching.url,vm.saveMatching.params,function (response) {
                    if(response.success){
                        vm.$emit("currentTab2");
                    }
                },function (error) {
                    console.log(error);
                });
            },
            getSalesLeadsById(id){
                let vm = this,params={
                    salesLeadsId:"",
                    realname:"",
                    sex:"男",
                    phone:"",
                    qq:"",
                    wechat:"",
                    email:"",
                    address:"",
                    otherInfoName:"",
                    otherInfoContent:"",
                    updateUser:""
                };
                vm.receiveMatchingTask.result={};
                vm.saveMatching.params=params;
                $(".city").selectpicker("val","").selectpicker("refresh");
                $('input[type=radio]').iCheck("destory");
                vm.post(vm.getSalesLeads.url,id,function (response) {
                    if(response.success){
                        let result=response.data;
                        let reSaveResult={
                            salesLeadsId:result.id,
                            realname:result.realname,
                            sex:result.sex,
                            phone:result.phone,
                            qq:result.qq,
                            wechat:result.wechat,
                            email:result.email,
                            address:result.address,
                            otherInfoName:result.otherInfoName,
                            otherInfoContent:result.otherInfoContent,
                            updateUser:result.updateUser
                        };
                        let addressArr=result.address.split('-');
                        let index=vm.sheng.indexOf(addressArr[0]);
                        vm.shi=data.citySearch.GT[index];
                        let index2=vm.shi.indexOf(addressArr[1]);
                        vm.xian=data.citySearch.GC[index][index2];
                        setTimeout(()=>{
                            $("#sheng").selectpicker("refresh").selectpicker("val",addressArr[0]);
                            $("#shi").selectpicker("refresh").selectpicker("val",addressArr[1]);
                            $("#xian").selectpicker("refresh").selectpicker("val",addressArr[2]);
                            vm.searchCon.shengVal=addressArr[0];
                            vm.searchCon.shiVal=addressArr[1];
                            vm.searchCon.xianVal=addressArr[2];
                        },300);
                        result.publishDate=new Date(response.data.publishDate).Format("yyyy-MM-dd hh:mm:ss");
                        vm.receiveMatchingTask.result=result;
                        vm.saveMatching.params=reSaveResult;
                        setTimeout(()=>{
                            $("input[type=radio]").iCheck({
                                radioClass : 'iradio_square-blue',
                            }).on("ifChecked",function () {
                                vm.saveMatching.params.sex=$(this).val();
                            });
                            let shiIndex,xianIndex;
                            shiIndex=vm.searchData.citySearch.GP.indexOf(vm.searchCon.shengVal);
                            $("#sheng").on("changed.bs.select",function (e,clickedIndex) {
                                shiIndex=clickedIndex-1;
                                vm.shi=vm.searchData.citySearch.GT[shiIndex];
                            }).on("hide.bs.select",function () {
                                $("#shi").selectpicker("refresh").selectpicker('val', '');
                                $("#xian").selectpicker("refresh").selectpicker('val', '');
                            });
                            $("#shi").on("changed.bs.select",function (e,clickedIndex) {
                                xianIndex=clickedIndex-1;
                                vm.xian=vm.searchData.citySearch.GC[shiIndex][xianIndex];
                            }).on("hide.bs.select",function () {
                                $("#xian").selectpicker("refresh").selectpicker('val', '');
                            });
                        },300);
                        vm.getMatchingNumber();
                    }
                },function (error) {
                    console.log(error);
                });
            }
        },
        mounted(){
            let vm=this;
            $("input[type=radio]").iCheck({
                radioClass : 'iradio_square-blue',
            }).on("ifChecked",function () {
                vm.saveMatching.params.sex=$(this).val();
            });
            $(".selectpicker").selectpicker({
                style: 'btn-default',
                size: 4
            });
            if(sessionStorage.getItem("salesLeadsId")){
                $(".reMatching-btn-box").removeClass("hide");
                $(".matching-btn-box").addClass("hide");
                vm.getSalesLeadsById(sessionStorage.getItem("salesLeadsId"));
            }else {
                let shiIndex,xianIndex;
                $("#sheng").on("changed.bs.select",function (e,clickedIndex) {
                    shiIndex=clickedIndex-1;
                    vm.shi=vm.searchData.citySearch.GT[shiIndex];
                }).on("hide.bs.select",function () {
                    $("#shi").selectpicker("refresh").selectpicker('val', '');
                    $("#xian").selectpicker("refresh").selectpicker('val', '');
                });
                $("#shi").on("changed.bs.select",function (e,clickedIndex) {
                    xianIndex=clickedIndex-1;
                    vm.xian=vm.searchData.citySearch.GC[shiIndex][xianIndex];
                }).on("hide.bs.select",function () {
                    $("#xian").selectpicker("refresh").selectpicker('val', '');
                });
                vm.getList();
            }
        }
    }
</script>