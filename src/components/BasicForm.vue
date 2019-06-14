<template>
<div>
  <!-- Basic Form for users to input the following items -->
    <el-form :model="ruleForm" :rules="rules" ref="ruleForm" class="demo-ruleForm" show="openDialog === false">
  <!-- Input first name in the form-->
  <el-form-item label="First Name" prop="firstName">
    <el-input v-model="ruleForm.firstName" placeholder="Mia"></el-input>
  </el-form-item>
  <!-- Input last name in the form -->
    <el-form-item label="Last Name" prop="lastName">
    <el-input v-model="ruleForm.lastName" placeholder="Welsh"></el-input>
  </el-form-item>
  <!-- Input email in the form -->
      <el-form-item label="Email" prop="email">
    <el-input v-model="ruleForm.email" placeholder="mia.welsh@hotmail.com"></el-input>
  </el-form-item>
  <!-- Input subject in the form -->
        <el-form-item label="Subject" prop="subject">
    <el-input v-model="ruleForm.subject" placeholder="Subject"></el-input>
  </el-form-item>
  <!-- Input claim content in the form -->
  <el-form-item label="Claim Content" prop="desc">
    <el-input type="textarea" v-model="ruleForm.desc" placeholder="Insert any additional information here..."></el-input>
  </el-form-item>
  <!-- user's checkbox to agree -->
      <el-form-item prop="checkBox">
        <el-checkbox label="I agree to the terms" v-model="ruleForm.checkBox"></el-checkbox>
      </el-form-item>
  <!-- once form is completed, user's must click the submit button -->
      <el-button type="primary" @click="submitForm('ruleForm')">Submit</el-button>
</el-form>
<!-- pop up alert message once completed form is submitted -->
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
    </div>
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
      // following list items
      ruleForm: {
        firstName: "",
        lastName: "",
        email: "",
        subject: "",
        desc: "",
        checkBox: []
      },
      // user's textbox to fill in 
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
          // user's must check the checkbox to agree
          checkBox: [
            { required: true, message: 'Please agree to the terms', trigger: 'change' }
          ]
        },
      openDialog: false
      };
    },
    // submit button
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
    // resets after submitting
    resetForm(formName) {
      this.$refs[formName].resetFields();
    }
  }
};
</script>

<style lang="scss">

// style for pop up alert message

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
