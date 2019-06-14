<template>
    <el-form :model="ruleForm" :rules="rules" ref="ruleForm" class="demo-ruleForm" show="openDialog === false">
  <el-form-item label="First Name" prop="firstName">
    <el-input v-model="ruleForm.firstName" placeholder="Mia"></el-input>
  </el-form-item>
    <el-form-item label="Last Name" prop="lastName">
    <el-input v-model="ruleForm.lastName" placeholder="Welsh"></el-input>
  </el-form-item>
      <el-form-item label="Email" prop="email">
    <el-input v-model="ruleForm.email" placeholder="mia.welsh@hotmail.com"></el-input>
  </el-form-item>
        <el-form-item label="Subject" prop="subject">
    <el-input v-model="ruleForm.subject" placeholder="Subject"></el-input>
  </el-form-item>
  <el-form-item label="Claim Content" prop="desc">
    <el-input type="textarea" v-model="ruleForm.desc" placeholder="Insert any additional information here..."></el-input>
  </el-form-item>
      <el-form-item prop="checkBox">
        <el-checkbox label="I agree to the terms" v-model="ruleForm.checkBox"></el-checkbox>
      </el-form-item>
      <el-button type="primary" @click="submitForm('ruleForm')">Submit</el-button>
      <el-dialog :visible.sync="openDialog">
      <div class="dialog-container">
        <ul>
          <li><strong>First Name:</strong></li>
          <li><strong>Last Name:</strong></li>
          <li><strong>Email:</strong></li>
          <li><strong>Subject:</strong></li>
          <li><strong>Claim Content:</strong></li>
        </ul>
        <ul>
          <li>{{ ruleForm.firstName }}</li>
          <li>{{ ruleForm.lastName }}</li>
          <li>{{ ruleForm.email }}</li>
          <li>{{ ruleForm.subject }}</li>
          <li>{{ ruleForm.desc }}</li>
        </ul>
      </div>
    </el-dialog>
</el-form>
</template>

<script>
export default {
  name: "contactForm",
  props: {
  msg: String
  },
  data: function() {
    var wordCount = (rule, value, callback) => {
      if (value.split(' ').length >= 30) {
        callback(new Error('Subject can not be more than 30 words'));
      } else {
        callback();
      }
    };
    return {
      ruleForm: {
        firstName: "",
        lastName: "",
        email: "",
        subject: "",
        desc: "",
        checkBox: []
      },
        rules: {
          firstName: [
            { required: true, message: 'Please input First Name', trigger: 'blur' },
          ],
          lastName: [
            { required: true, message: 'Please input Last Name', trigger: 'blur' },
          ],
          email: [
            { required: true, message: 'Please input email', trigger: 'blur' },
          ],
          subject: [
            { required: true, message: 'Please input subject', trigger: 'blur' },
          {
            validator: wordCount,
            trigger: "blur"
          }
          ],
          checkBox: [
            { required: true, message: 'Please agree to the terms', trigger: 'change' }
          ],
      openDialog: false
        }
      };
    },
      methods: {
    submitForm(formName) {
      this.$refs[formName].validate(valid => {
        if (valid) {
          this.openDialog = true;
        } else {
          return false;
        }
      });
    },
    resetForm(formName) {
      this.$refs[formName].resetFields();
    }
  }
};
</script>

<style lang="scss">
.container {
  margin: auto 50px;
}

.dialog-container {
  display: flex;
  margin: auto 20px;
  text-align: left;

  ul {
    list-style: none;
  }
}
</style>
