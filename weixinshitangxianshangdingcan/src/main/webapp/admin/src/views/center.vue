<template>
  <div>
    <el-form
      class="detail-form-content"
      ref="ruleForm"
      :model="ruleForm"
      label-width="80px"
    >  
     <el-row>
                    <el-col :span="12">
           <el-form-item v-if="flag=='shangjia'"  label='商家名称' prop="shangjiaName">
               <el-input v-model="ruleForm.shangjiaName"  placeholder='商家名称' clearable></el-input>
           </el-form-item>
         </el-col>

         <el-col :span="12">
           <el-form-item v-if="flag=='shangjia'"  label='联系方式' prop="shangjiaPhone">
               <el-input v-model="ruleForm.shangjiaPhone"  placeholder='联系方式' clearable></el-input>
           </el-form-item>
         </el-col>

         <el-col :span="12">
           <el-form-item v-if="flag=='shangjia'"  label='邮箱' prop="shangjiaEmail">
               <el-input v-model="ruleForm.shangjiaEmail"  placeholder='邮箱' clearable></el-input>
           </el-form-item>
         </el-col>

         <el-col :span="12">
             <el-form-item v-if="flag=='shangjia'" label='营业执照展示' prop="shangjiaPhoto">
                 <file-upload
                         tip="点击上传照片"
                         action="file/upload"
                         :limit="3"
                         :multiple="true"
                         :fileUrls="ruleForm.shangjiaPhoto?ruleForm.shangjiaPhoto:''"
                         @change="shangjiaPhotoUploadChange"
                 ></file-upload>
             </el-form-item>
         </el-col>
         <el-col :span="12">
             <el-form-item v-if="flag=='shangjia'"  label='商家星级类型' prop="shangjiaXingjiTypes">
                 <el-select v-model="ruleForm.shangjiaXingjiTypes" disabled placeholder='请选择商家星级类型'>
                     <el-option
                             v-for="(item,index) in shangjiaXingjiTypesOptions"
                             v-bind:key="item.codeIndex"
                             :label="item.indexName"
                             :value="item.codeIndex">
                     </el-option>
                 </el-select>
             </el-form-item>
         </el-col>
         <el-col :span="12">
             <el-form-item v-if="flag=='shangjia'"  label='现有余额' prop="newMoney">
                 <el-input v-model="ruleForm.newMoney"  placeholder='现有余额' disabled ></el-input>
             </el-form-item>
         </el-col>
         <el-col :span="24">
             <el-form-item v-if="flag=='shangjia'"  label="商家简介" prop="shangjiaContent">
                 <editor
                         style="min-width: 200px; max-width: 600px;"
                         v-model="ruleForm.shangjiaContent"
                         class="editor"
                         action="file/upload">
                 </editor>
             </el-form-item>
         </el-col>
         <el-col :span="12">
           <el-form-item v-if="flag=='yonghu'"  label='用户姓名' prop="yonghuName">
               <el-input v-model="ruleForm.yonghuName"  placeholder='用户姓名' clearable></el-input>
           </el-form-item>
         </el-col>

         <el-col :span="12">
           <el-form-item v-if="flag=='yonghu'"  label='用户手机号' prop="yonghuPhone">
               <el-input v-model="ruleForm.yonghuPhone"  placeholder='用户手机号' clearable></el-input>
           </el-form-item>
         </el-col>

         <el-col :span="12">
           <el-form-item v-if="flag=='yonghu'"  label='用户身份证号' prop="yonghuIdNumber">
               <el-input v-model="ruleForm.yonghuIdNumber"  placeholder='用户身份证号' clearable></el-input>
           </el-form-item>
         </el-col>

         <el-col :span="12">
             <el-form-item v-if="flag=='yonghu'" label='用户头像' prop="yonghuPhoto">
                 <file-upload
                         tip="点击上传照片"
                         action="file/upload"
                         :limit="3"
                         :multiple="true"
                         :fileUrls="ruleForm.yonghuPhoto?ruleForm.yonghuPhoto:''"
                         @change="yonghuPhotoUploadChange"
                 ></file-upload>
             </el-form-item>
         </el-col>
         <el-col :span="12">
           <el-form-item v-if="flag=='yonghu'"  label='电子邮箱' prop="yonghuEmail">
               <el-input v-model="ruleForm.yonghuEmail"  placeholder='电子邮箱' clearable></el-input>
           </el-form-item>
         </el-col>

         <el-col :span="12">
             <el-form-item v-if="flag=='yonghu'"  label='会员等级' prop="huiyuandengjiTypes">
                 <el-select v-model="ruleForm.huiyuandengjiTypes" disabled placeholder='请选择会员等级'>
                     <el-option
                             v-for="(item,index) in huiyuandengjiTypesOptions"
                             v-bind:key="item.codeIndex"
                             :label="item.indexName"
                             :value="item.codeIndex">
                     </el-option>
                 </el-select>
             </el-form-item>
         </el-col>
         <el-col :span="12">
             <el-form-item v-if="flag=='yonghu'"  label='余额' prop="newMoney">
                 <el-input v-model="ruleForm.newMoney"  placeholder='余额' disabled ></el-input>
             </el-form-item>
         </el-col>
         <el-form-item v-if="flag=='users'" label="用户名" prop="username">
             <el-input v-model="ruleForm.username"
                       placeholder="用户名"></el-input>
         </el-form-item>
         <el-col :span="12">
             <el-form-item v-if="flag=='yonghu'"  label="性别" prop="sexTypes">
                 <el-select v-model="ruleForm.sexTypes" placeholder="请选择性别">
                     <el-option
                             v-for="(item,index) in sexTypesOptions"
                             v-bind:key="item.codeIndex"
                             :label="item.indexName"
                             :value="item.codeIndex">
                     </el-option>
                 </el-select>
             </el-form-item>
         </el-col>
         <el-col :span="24">
             <el-form-item>
                 <el-button type="primary" @click="onUpdateHandler">修 改</el-button>
             </el-form-item>
         </el-col>
     </el-row>
    </el-form>
  </div>
</template>
<script>
// 数字，邮件，手机，url，身份证校验
import { isNumber,isIntNumer,isEmail,isMobile,isPhone,isURL,checkIdCard } from "@/utils/validate";

export default {
  data() {
    return {
      ruleForm: {},
      flag: '',
      usersFlag: false,
      sexTypesOptions : [],
     shangjiaXingjiTypesOptions : [],
     huiyuandengjiTypesOptions : [],
    };
  },
  mounted() {
    //获取当前登录用户的信息
    var table = this.$storage.get("sessionTable");
    this.sessionTable = this.$storage.get("sessionTable");
    this.role = this.$storage.get("role");
    if (this.role != "管理员"){
    }

    this.flag = table;
    this.$http({
      url: `${this.$storage.get("sessionTable")}/session`,
      method: "get"
    }).then(({ data }) => {
      if (data && data.code === 0) {
        this.ruleForm = data.data;
      } else {
        this.$message.error(data.msg);
      }
    });
      this.$http({
          url: `dictionary/page?page=1&limit=100&sort=&order=&dicCode=sex_types`,
          method: "get"
      }).then(({ data }) => {
          if (data && data.code === 0) {
          this.sexTypesOptions = data.data.list;
      } else {
          this.$message.error(data.msg);
      }
  });
   this.$http({
       url: `dictionary/page?page=1&limit=100&sort=&order=&dicCode=shangjia_xingji_types`,
       method: "get"
   }).then(({ data }) => {
       if (data && data.code === 0) {
          this.shangjiaXingjiTypesOptions = data.data.list;
      } else {
          this.$message.error(data.msg);
      }
    });
   this.$http({
       url: `dictionary/page?page=1&limit=100&sort=&order=&dicCode=huiyuandengji_types`,
       method: "get"
   }).then(({ data }) => {
       if (data && data.code === 0) {
          this.huiyuandengjiTypesOptions = data.data.list;
      } else {
          this.$message.error(data.msg);
      }
    });
  },
  methods: {
    shangjiaPhotoUploadChange(fileUrls) {
        this.ruleForm.shangjiaPhoto = fileUrls;
    },
    yonghuPhotoUploadChange(fileUrls) {
        this.ruleForm.yonghuPhoto = fileUrls;
    },

    onUpdateHandler() {
                         if((!this.ruleForm.shangjiaName)&& 'shangjia'==this.flag){
                             this.$message.error('商家名称不能为空');
                             return
                         }

                         if((!this.ruleForm.shangjiaPhone)&& 'shangjia'==this.flag){
                             this.$message.error('联系方式不能为空');
                             return
                         }

                             if( 'shangjia' ==this.flag && this.ruleForm.shangjiaEmail&&(!isEmail(this.ruleForm.shangjiaEmail))){
                                 this.$message.error(`邮箱应输入邮箱格式`);
                                 return
                             }
                         if((!this.ruleForm.shangjiaPhoto)&& 'shangjia'==this.flag){
                             this.$message.error('营业执照展示不能为空');
                             return
                         }

                         if((!this.ruleForm.shangjiaXingjiTypes)&& 'shangjia'==this.flag){
                             this.$message.error('商家星级类型不能为空');
                             return
                         }

                         if((!this.ruleForm.shangjiaContent)&& 'shangjia'==this.flag){
                             this.$message.error('商家简介不能为空');
                             return
                         }

                         if((!this.ruleForm.yonghuName)&& 'yonghu'==this.flag){
                             this.$message.error('用户姓名不能为空');
                             return
                         }

                             if( 'yonghu' ==this.flag && this.ruleForm.yonghuPhone&&(!isMobile(this.ruleForm.yonghuPhone))){
                                 this.$message.error(`手机应输入手机格式`);
                                 return
                             }
                         if((!this.ruleForm.yonghuIdNumber)&& 'yonghu'==this.flag){
                             this.$message.error('用户身份证号不能为空');
                             return
                         }

                         if((!this.ruleForm.yonghuPhoto)&& 'yonghu'==this.flag){
                             this.$message.error('用户头像不能为空');
                             return
                         }

                             if( 'yonghu' ==this.flag && this.ruleForm.yonghuEmail&&(!isEmail(this.ruleForm.yonghuEmail))){
                                 this.$message.error(`邮箱应输入邮箱格式`);
                                 return
                             }
                         if((!this.ruleForm.huiyuandengjiTypes)&& 'yonghu'==this.flag){
                             this.$message.error('会员等级不能为空');
                             return
                         }

        if((!this.ruleForm.sexTypes)&& this.flag !='users'){
            this.$message.error('性别不能为空');
            return
        }
      if('users'==this.flag && this.ruleForm.username.trim().length<1) {
        this.$message.error(`用户名不能为空`);
        return	
      }
      this.$http({
        url: `${this.$storage.get("sessionTable")}/update`,
        method: "post",
        data: this.ruleForm
      }).then(({ data }) => {
        if (data && data.code === 0) {
          this.$message({
            message: "修改信息成功",
            type: "success",
            duration: 1500,
            onClose: () => {
            }
          });
        } else {
          this.$message.error(data.msg);
        }
      });
    }
  }
};
</script>
<style lang="scss" scoped>
</style>
