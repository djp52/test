---

title: Maths Challenge

---

<!-- VUE -->
<script src="https://cdn.jsdelivr.net/npm/vue@2"></script>

# Elsa's Maths Challenge


{% raw %}
<div id="app-maths" style="font-size:xx-large">

    <p>Maths</p>
    <p>{{x1}} {{symbol}} {{x2}}</p>
    <p><input type="string" v-model="myAnswer" disabled="true"/></p>
    <p><button v-on:click="myAnswer += '1'"><span style="width:3em;text-align:center">1</span></button>
    <button v-on:click="myAnswer += '2'"><span style="width:3em;text-align:center">2</span></button>
    <button v-on:click="myAnswer += '3'"><span style="width:3em;text-align:center">3</span></button></p>
    <p><button v-on:click="myAnswer += '4'"><span style="width:3em;text-align:center">4</span></button>
    <button v-on:click="myAnswer += '5'"><span style="width:3em;text-align:center">5</span></button>
    <button v-on:click="myAnswer += '6'"><span style="width:3em;text-align:center">6</span></button></p>
    <p><button v-on:click="myAnswer += '7'"><span style="width:3em;text-align:center">7</span></button>
    <button v-on:click="myAnswer += '8'"><span style="width:3em;text-align:center">8</span></button>
    <button v-on:click="myAnswer += '9'"><span style="width:3em;text-align:center">9</span></button></p>
    <p><button style="color:lightcoral;" v-on:click="d"><span style="width:3em;text-align:center">⌫</span></button>
    <button v-on:click="myAnswer += '0'"><span style="width:3em;text-align:center">0</span></button>
    <button style="color:lightgreen" v-on:click="check_answer"><span style="width:3em;text-align:center">✓</span></button></p>
    <p><button style="color:lightskyblue" v-on:click="n">Next Question</button></p>
    <p>{{ message }}</p>
    <p style="font-size:large">You have {{ correct }} answers right</p>
</div>

{% endraw %}

<script>

var maths = new Vue ({
    el: '#app-maths', 

    mounted:function(){
        this.generate_question() },

    data: {
      myAnswer : "",
      answer : 2,
      n_min : 1,
      n_max : 12,
      t_min : 1,
      t_max : 7,
      x1 : 1,
      x2 : 1,
      message : "Type and answer and press ✓",
      dis : true,
      symbol : "+",
      correct : 0
    },
    methods : {
      d : function () { this.myAnswer = this.myAnswer.slice(0, -1); },
  
      check_answer : function () {
          if (this.answer == parseInt(this.myAnswer, null)) {   
              this.message = "Correct";
              this.correct = this.correct + 1;
              this.dis = false;
              }
          else{
              this.message = "Not quite right - try again!";
              this.myAnswer = "";
          }        
      },
      
      n : function () {
          this.myAnswer = "";
          this.generate_question();
          this.dis = true;
      },
  
      generate_question : function () {
          // Pick a type
          var a = Math.floor(Math.random() * 4);
          switch (a) {
           case 0:
              // Add
              this.x1 = Math.floor(Math.random() * (this.n_max - this.n_min)) + this.n_min;
              this.x2 = Math.floor(Math.random() * (this.n_max - this.n_min)) + this.n_min;
              this.symbol = "+";
              this.answer = this.x1 + this.x2;
              break;
           case 1:
              // Subtract
              this.x1 = Math.floor(Math.random() * (this.n_max - this.n_min)) + this.n_min;
              this.x2 = Math.floor(Math.random() * (this.x1 - this.n_min)) + this.n_min;
              this.symbol = "-";
              this.answer = this.x1 - this.x2;
              break;
           case 2:
              // Multiply
              this.x1 = Math.floor(Math.random() * (this.n_max - this.n_min)) + this.n_min;
              this.x2 = Math.floor(Math.random() * (this.t_max - this.t_min)) + this.t_min;
              this.symbol = "×";
              this.answer = this.x1 * this.x2;
              break;
           case 3:
              // Divide
              this.answer = Math.floor(Math.random() * (this.t_max - this.t_min)) + this.n_min;
              this.x2 = Math.floor(Math.random() * (this.t_max - this.t_min)) + this.n_min;
              this.symbol = "÷";
              this.x1 = this.answer * this.x2;
              break;
          }
          return null
          
      }}});


</script>
