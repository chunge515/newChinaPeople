<template>
  <div class="editAuditionBox padTop20">
    <div class="stu-body">
      <el-row v-if="tmpUserInfo">
        <el-col :span="24">
          <el-row>
            <el-col :span="3">预约三次试听时间：</el-col>
            <el-col :span="21">{{auditionRecordObj.appointmentDatetime | convertDate}}</el-col>
          </el-row>
        </el-col>
        <el-col :span="8">
          <el-row>
            <el-col :span="9">是否完成三次试听：</el-col>
            <el-col :span="15">{{auditionRecordObj.hasComplete=="0"?"否":"是"}}</el-col>
          </el-row>
        </el-col>
        <el-col :span="12">
          <el-row>
            <el-col :span="6">三次试听干预导师：</el-col>
            <el-col :span="18">{{auditionRecordObj.serviceTutorialName }}</el-col>
          </el-row>
        </el-col>
        <el-col :span="8">
          <el-row>
            <el-col :span="9">用户意向等级：</el-col>
            <el-col :span="15">{{auditionRecordObj.intentionLevel}}</el-col>
          </el-row>
        </el-col>
        <el-col :span="12">
          <el-row>
            <el-col :span="6">切单情况：</el-col>
            <el-col :span="18">{{commeCut[auditionRecordObj.cutListState]}} <span v-if="auditionRecordObj.cutListState>1">原因：{{auditionRecordObj.cutListReason}}</span></el-col>
          </el-row>
        </el-col>
        <el-col :span="24">
          <el-row>
            <el-col :span="3">三次试听科目及内容：</el-col>
            <el-col :span="21">
              <p>{{commonSubject[auditionRecordObj.auditionSubjectCode] }}</p>
              <p>{{auditionRecordObj.auditionContent}}</p>
            </el-col>
          </el-row>
        </el-col>
        <el-col :span="8">
          <el-row>
            <el-col :span="9">是否报名：</el-col>
            <el-col :span="15">{{auditionRecordObj.signUpState | isF}}</el-col>
          </el-row>
        </el-col>
        <el-col :span="24" v-if="auditionRecordObj.signUpState=='1'">
          <el-row>
            <el-col :span="8">
              <el-row>
                <el-col :span="9">报名学科：</el-col>
                <el-col :span="15">
                  <span v-for="(item,index) in auditionRecordObj.signUpSubjectCodes">{{commonSubject[item]}}</span>
                </el-col>
              </el-row>
            </el-col>
            <el-col :span="8">
              <el-row>
                <el-col :span="9">报名课时：</el-col>
                <el-col :span="15">{{auditionRecordObj.signUpState | isF}}</el-col>
              </el-row>
            </el-col>
            <el-col :span="8">
              <el-row>
                <el-col :span="9">开课日期时间：</el-col>
                <el-col :span="15">{{auditionRecordObj.courseBeginDatetime | convertDate}}</el-col>
              </el-row>
            </el-col>
            <el-col :span="8">
              <el-row>
                <el-col :span="9">缴费金额：</el-col>
                <el-col :span="15">{{auditionRecordObj.paymentAmount}}</el-col>
              </el-row>
            </el-col>
            <el-col :span="8">
              <el-row>
                <el-col :span="9">缴费日期：</el-col>
                <el-col :span="15">{{auditionRecordObj.paymentDatetime | convertDate}}</el-col>
              </el-row>
            </el-col>
            <el-col :span="8">
              <el-row>
                <el-col :span="9">是否签署协议：</el-col>
                <el-col :span="15">{{auditionRecordObj.hasProtocol | isF}}</el-col>
              </el-row>
            </el-col>
            <el-col :span="8">
              <el-row>
                <el-col :span="9">协议编号：</el-col>
                <el-col :span="15">{{auditionRecordObj.protocolNumber}}</el-col>
              </el-row>
            </el-col>
            <el-col :span="8">
              <el-row>
                <el-col :span="9">确认协议到账：</el-col>
                <el-col :span="15">{{auditionRecordObj.protocolAccount | isF}}</el-col>
              </el-row>
            </el-col>
          </el-row>
        </el-col>
        <el-col :span="24">
          <el-row>
            <el-col :span="3">享受折扣/优惠套餐：</el-col>
            <el-col :span="21">{{auditionRecordObj.discountPackage}}</el-col>
          </el-row>
        </el-col>
        <el-col :span="24">
          <el-row>
            <el-col :span="3">其他备注信息：</el-col>
            <el-col :span="21">{{auditionRecordObj.remark}}</el-col>
          </el-row>
        </el-col>




        <el-col :span="24"><h5>一次试听学生反馈</h5></el-col>
        <el-col :span="12">
          <el-row>
            <el-col :span="6">干预训练素材难度：</el-col>
            <el-col :span="18">{{commeDifficulty[auditionRecordObj.studentFeedbackDifficulty]}}</el-col>
          </el-row>
        </el-col>
        <el-col :span="12">
          <el-row>
            <el-col :span="8">对干预训练方法接受程度：</el-col>
            <el-col :span="16">{{commeAccept[auditionRecordObj.studentFeedbackAccept] }}</el-col>
          </el-row>
        </el-col>
        <el-col :span="12">
          <el-row>
            <el-col :span="6">上课过程中：</el-col>
            <el-col :span="18">{{commeThink[auditionRecordObj.studentFeedbackThink]}}</el-col>
          </el-row>
        </el-col>
        <el-col :span="12">
          <el-row>
            <el-col :span="8">本次干预效果：</el-col>
            <el-col :span="16">{{commeEffect[auditionRecordObj.studentFeedbackEffect]}}</el-col>
          </el-row>
        </el-col>
        <el-col :span="24">
          <el-row>
            <el-col :span="3">备注：</el-col>
            <el-col :span="21">{{auditionRecordObj.studentFeedbackRemark}}</el-col>
          </el-row>
        </el-col>
        <el-col :span="24"><h5>一次试听教师评价</h5></el-col>
        <el-col :span="12">
          <el-row>
            <el-col :span="6">学生的学习习惯：</el-col>
            <el-col :span="18">{{commeHabit[auditionRecordObj.teacherAssessmentStudyHabit]}}</el-col>
          </el-row>
        </el-col>
        <el-col :span="12">
          <el-row>
            <el-col :span="8">学生对干预方法的适应程度：</el-col>
            <el-col :span="16">{{commeTeaAdapt[auditionRecordObj.teacherAssessmentMethodAdapt]}}</el-col>
          </el-row>
        </el-col>
        <el-col :span="24">
          <el-row>
            <el-col :span="4">学生有哪些不好的习惯：</el-col>
            <el-col :span="20"><span v-for="(item,index) in auditionRecordObj.teacherAssessmentBadHabits" :key="index">{{commeBadHabits[item]}}</span></el-col>
          </el-row><!---->
        </el-col>
        <el-col :span="12">
          <el-row>
            <el-col :span="9">学生的学习方法：</el-col>
            <el-col :span="15">{{commeStudyMethod[auditionRecordObj.teacherAssessmentStudyMethod]}}</el-col>
          </el-row>
        </el-col>
        <el-col :span="12">
          <el-row>
            <el-col :span="9">学生的思维能力：</el-col>
            <el-col :span="15">{{commeAbility[auditionRecordObj.teacherAssessmentThinkAbility]}}</el-col>
          </el-row>
        </el-col>
        <el-col :span="12">
          <el-row>
            <el-col :span="9">知识掌握情况：</el-col>
            <el-col :span="15">{{commeKnowledge[auditionRecordObj.teacherAssessmentMasterKnowledge]}}</el-col>
          </el-row>
        </el-col>
        <el-col :span="24">
          <el-row>
            <el-col :span="3">备注：</el-col>
            <el-col :span="15">{{auditionRecordObj.teacherAssessmentRemark}}</el-col>
          </el-row>
        </el-col>
      </el-row>
      <div class="addBtn">
        <el-button type="primary" @click="go()">编辑</el-button>
      </div>
    </div>
  </div>
</template>
<script>
  import moment from "moment"
  export default {
    data() {
      return {
        //当前学生的信息
        tmpUserInfo:null,
        auditionRecordObj:{},
        type:'',
        commeCut:{
          "1":'意向强烈，已报名',
          "2":'意向强烈，未报名',
          "3":'无意向，未报名'
        },
        commeHabit:{
          "1":'较好',
          "2":'一般',
          "3":'较差'
        },
        commeAdapt:{
          "1":'较好',
          "2":'一般',
          "3":'较差'
        },
        commeTeaAdapt:{
          "1":'非常适应',
          "2":'一般',
          "3":'勉强适应'
        },
        commeStudyMethod:{
          "1":'未掌握有效的学习方法',
          "2":'有方法但是一般',
          "3":'有有效的学习方法'
        },
        commeAbility:{
          "1":'需教师多次引导',
          "2":'需教师适当引导',
          "3":'思维敏捷,反应较快'
        },
        commeKnowledge:{
          "1":'基础知识掌握一般解决复杂问题有困难',
          "2":'基础知识扎实但解决复杂问题有困难',
          "3":'基础知识扎实能解决复杂问题'
        },
      };
    },
    props: {},
    methods: {
      //获取试听记录
      getStudentAuditionRecords(){
        var $this=this;
        var obj={
          studentId:$this.tmpUserInfo.userId,
          auditionNumber:3
        }
        this.$axios
          .post("/student/getStudentAuditionRecords",obj)
          .then(res => {
            if(res.code=="000000"){
              var result=res.result || [];
              if(result.length>0){
                var obj=result[0];
                obj.assessmentResult = JSON.parse(obj.assessmentResult);
                obj.teacherAssessmentBadHabits = JSON.parse(obj.teacherAssessmentBadHabits);
                obj.signUpSubjectCodes = JSON.parse(obj.signUpSubjectCodes);

                $this.auditionRecordObj=obj;
              }else{
                $this.$router.push({path:'/editAuditionB/add'})
              }

              // this.$router.push({path:"/studentMange"})
            }else{
              this.$message({
                type: 'warning',
                message: res.message
              });
            }
          })
          .catch(err => {
            this.$message({
              type: 'info',
              message: "保存失败"
            });
          });
      },
      go(){
        this.localData.set('auditionRecordObjT',this.auditionRecordObj)
        this.$router.push({path:'/editAuditionB/add',query:{edit:1}})
      },

    },
    mounted() {
      var $this=this;
      $this.tmpUserInfo = $this.localData.get('tmpStudentInfo');
      $this.getStudentAuditionRecords()

    },
    watch:{
      "$route": "getStudentAuditionRecords"
    },
    filters: {
      sexFilter(v) {
        switch (v) {
          case 0:
            return "女";
          case 1:
            return "男";
          default:
            return "";
        }
      },
      convertDate(v){
        return v =  moment(v).format("YYYY-MM-DD HH:mm:ss");
      },
      isF(v){
        switch (v) {
          case "0":
            return "否";
          case "1":
            return "是";
          default:
            return "";
        }
      },
      timeFilter(v,f){
        return v&&moment(v).format(f)||v;
      }
    }
  }
</script>
<style type="text/css" lang="scss" scoped>
  .subBook{
    padding-right: 20px;
  }
  .stu-body {
    .el-row {
      .el-row {
        padding-bottom: 26px;
      }
    }
  }

  .childs {
    border-top: 1px solid #d6e1f1;
  }

  .routers {
    border-left: 1px solid #d6e1f1;
    border-right: 1px solid #d6e1f1;
    -ms-user-select: none;
    -webkit-user-select: none;
    user-select: none;
    padding: 0 !important;
    ul {
      padding: 0;
    }
    li {
      border-bottom: 1px solid #d6e1f1;;
      padding: 16px 10px;
      cursor: pointer;
      &.active {
        background-color: #1DA4DE;
        color: #ffffff;
      }
    }
  }
</style>
<style type="text/css" lang="scss">
  .editAuditionBox{
    h5{
      font-size: 18px;
      font-weight: normal;
      line-height:40px;
      color: #f00;
      // border-bottom: 1px solid #ccc;
      margin-bottom:30px;
    }
    span{
      margin-right:10px;}
    .addBtn{
      margin-bottom:20px;
      text-align: center;
    }
  }
</style>
