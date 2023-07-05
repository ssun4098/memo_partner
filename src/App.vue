<template>
  <div class="container main">
    <div class="fs-1">문제</div>
    <hr/>
    <div class="fs-3 mb-5">{{problem}}</div>
    <button @click="viewAnswer" class="btn btn-primary btn-lg">정답확인</button> <button class="btn btn-success btn-lg" @click="viewProblem">다른 문제</button>
    <div v-show="view" class="fs-3">{{answer}}</div>
    <hr/>

    <div class="fs-1">문제 등록</div>
    <div class="mb-3">
      <label for="input_problem" class="form-label">문제</label>
      <input type="text" id="input_problem" class="form-control form-control-lg" v-model="form.problem" style="font-weight : bold ;"/>
    </div>

    <div class="mb-3">
      <label for="input_answer" class="form-label">정답</label>
      <textarea id="input_answer" class="form-control form-control-lg" v-model="form.answer" style="font-weight : bold ;"/>
    </div>
    <button class="btn btn-primary" @click="insertProblem">등록</button>
  </div>
</template>

<script>

export default {
  name: 'App',
  mounted() {
    this.getProblems();
    this.viewProblem();
  },
  data() {
    return {
      problems: [],
      answers: [],
      problem: '',
      answer: '',
      view: false,
      form: {
        problem: '',
        answer: ''
      }
    }
  },
  methods: {
    getProblems() {
      for(let i = 0; i < localStorage.length; i++) {
        const problem = localStorage.key(i);
        this.problems.push(problem);
        this.answers.push(localStorage.getItem(problem));
      }
    },
    viewProblem() {
      const value = Math.floor(Math.random() * this.problems.length);
      this.problem = this.problems[value];
      this.answer = this.answers[value];
      this.view = false;
    },
    viewAnswer() {
      this.view = !this.view;
    },
    insertProblem() {
      if(this.form.problem !== '' && this.form.answer !== ''){
        localStorage.setItem(this.form.problem, this.form.answer);
      }
    }
  }
}
</script>

<style>

.main {
  font-weight: bold;
  font-family: "bemin",sans-serif;
}

@font-face {
  font-family: 'bemin';
  src:url("font/NotoSansKR-Regular.otf");
}
</style>
