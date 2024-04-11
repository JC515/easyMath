<script setup>
import {ref} from 'vue';

const question = ref('');
const userAnswer = ref('');

function generateQuestion() {
  const operators = ['+', '-', '*', '/'];
  let num1 = Math.floor(Math.random() * 100);
  let num2 = Math.floor(Math.random() * 100);
  let num3 = Math.floor(Math.random() * 100);
  let operator1 = operators[Math.floor(Math.random() * 4)];
  let operator2 = operators[Math.floor(Math.random() * 4)];

  let questionString = `${num1} ${operator1} ${num2} ${operator2} ${num3}`;

  let answer = checkAnswer(questionString);

  // 确保答案是整数且在 0-100 之间
  while (!Number.isInteger(answer) || answer > 100 || answer < 0) {
    // 重新生成题目
    num1 = Math.floor(Math.random() * 100);
    num2 = Math.floor(Math.random() * 100);
    num3 = Math.floor(Math.random() * 100);
    operator1 = operators[Math.floor(Math.random() * 4)];
    operator2 = operators[Math.floor(Math.random() * 4)];
    questionString = `${num1} ${operator1} ${num2} ${operator2} ${num3}`;
    answer = checkAnswer(questionString);
  }

  return questionString;
}

function checkAnswer(questionString) {
  // 使用 eval() 计算答案 (注意安全风险，这里假设输入安全)
  return eval(questionString);
}

function startQuestion() {
  question.value = generateQuestion();
  userAnswer.value = ''; // 清空答案输入框
}

function submitAnswer() {
  const correctAnswer = checkAnswer(question.value);
  if (Number(userAnswer.value) === correctAnswer) {
    alert('回答正确！🎉');
    startQuestion();
  } else {
    alert(`回答错误，正确答案是 ${correctAnswer}`);
  }
}
</script>

<template>
  <el-header style="height: 100px;">
    <h1 style="text-align: center;background-color: antiquewhite">小学生简单四则运算</h1>
  </el-header>
  <div style="margin-top: 10vh"></div>
  <el-main>
    <el-card style="max-width: 480px ;text-align: center;background-color: aquamarine">
      <p class="text item">{{ question }}</p>
      <el-input v-model="userAnswer" placeholder="请输入答案" style="margin-bottom: 30px"></el-input>
      <el-button type="primary" round @click="startQuestion">出题</el-button>
      <el-button type="primary" round @click="submitAnswer">提交</el-button>
    </el-card>
  </el-main>
</template>

<style scoped>
.el-main {
  display: flex;
  justify-content: center; /* 水平居中 */
  align-items: center; /* 垂直居中 */
}

.el-card {
  padding: 2em;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1); /* 添加阴影 */
}

.text.item {
  font-size: 1.2em;
  margin-bottom: 1em;
}

</style>
