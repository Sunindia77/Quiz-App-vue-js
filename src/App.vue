<template>
  <div class="container-app">
    <div class="container-quiz">
      <div class="quiz-header">
        <h1>Quiz App</h1>
      </div>
      <div class="main-quiz" v-for="(element, index) in questions.slice(a,b)" :key="index" v-show="quiz">
        <div class="box-question">
          <h2>Question{{b}}/{{questions.length}}</h2>
          <p>{{element.question}}</p>
        </div>
        <div class="box-suggestions">
          <ul>
            <li v-for="(item, index) in element.suggestions" :key="index" :class="select ? check(item) :''" @click="selectResponse(item)">{{item.suggestion}} <div class="fas fa-check" v-if="select ?item.isCorrect: ''"></div><div class="fas fa-times" v-if="select ?  !item.isCorrect: ''"></div></li>
          </ul>
        </div>
      </div>
      <div class="box-score" v-if="score_show">
        <h2>Your score is </h2>
        <h2>{{score}}/{{questions.length}}</h2>
        <div class="btn-restart">
          <button @click="restartQuiz">Restart <i class="fas fa-sync-alt"></i></button>
        </div>
      </div>
      <div class="quiz-footer">
        <div class="box-button">
          <button @click="skipQuestion" :style="!next ? 'background-color:rgb(106,128,202)' :''">Skip</button>
          <button @click="nextQuestion" :style="next ? 'background-color:rgb(106,128,202)' :''">Next</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data(){
    return{
      questions:[
        {
          question:'What is the capital of France?',
          suggestions:[
            {suggestion:'New York'},
            {suggestion:'London'},
            {suggestion:'Paris', isCorrect: true },
            {suggestion:'Dublin'},
          
          ]
        },
        {
          question:'Who is CEO of Tesla?',
          suggestions:[
            {suggestion:'Jeff Bezos'},
            {suggestion:'Elon Musk', isCorrect: true },
            {suggestion:'Bill Gates'},
            {suggestion:'Tony Star'},
          
          ]
        },
        {
          question:'The iPhone was created by which company?',
          suggestions:[
            {suggestion:'Apple', isCorrect: true},
            {suggestion:'Intel'},
            {suggestion:'Amazon'},
            {suggestion:'Microsoft'},
          
          ] 
        },
        {
          question:'How many Harry Potter books are there?',
          suggestions:[
            {suggestion:'1'},
            {suggestion:'4'},
            {suggestion:'6'},
            {suggestion:'7', isCorrect: true},
          
          ]
        },
        
      ],
      a:0,
      b:1,
      select:false,
      score:0,
      quiz:true,
      score_show: false,
      next:false,
    }
      
  },
  methods:{
    selectResponse(e){

      this.select = true;
      this.next=true;

      if (e.isCorrect){
        this.score++;
      }

    },
    check(status){
      if(status.isCorrect){
        return 'correct'
      }else{
        return 'incorrect'
      }

    },
    //Move forward with next button 
    nextQuestion(){
      if (!this.next) {
        return;
        
      }

      if(this.questions.length-1==this.a){
        this.score_show=true;
        this.quiz=false;
      } else{
        this.a++;
        this.b++;
        this.select = false ;
        this.next = false;

      }
    },
        //Skip up the Question 

    skipQuestion(){
      if (this.next) {
        return;
        
      } 


      if(this.questions.length-1== this.a){
        this.score_show= true;
        this.quiz=false;
      }else{
        this.a++;
        this.b++;

      }
    },
    // reset data
    restartQuiz(){

      Object.assign(this.$data, this.$options.data());
    }
  }
}
</script>
