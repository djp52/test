---

title: Maths Challenge

---

<!-- VUE -->
<script src="https://cdn.jsdelivr.net/npm/vue@2"></script>

# Elsa's Maths Challenge


{% raw %}
<div id="app-maths">

    <p>Maths</p>
    <p>{{x1}} {{symbol}} {{x2}}</p>
    <p><input type="string" v-model="myAnswer" disabled="true"/></p>
    <p><button v-on:click="myAnswer += '1'">1</button>
    <button v-on:click="myAnswer += '2'">2</button>
    <button v-on:click="myAnswer += '3'">3</button></p>
    <p><button v-on:click="myAnswer += '4'">4</button>
    <button v-on:click="myAnswer += '5'">5</button>
    <button v-on:click="myAnswer += '6'">6</button></p>
    <p><button v-on:click="myAnswer += '7'">7</button>
    <button v-on:click="myAnswer += '8'">8</button>
    <button v-on:click="myAnswer += '9'">9</button></p>
    <p><button style="color:lightcoral;" v-on:click="d">Del</button>
    <button v-on:click="myAnswer += '0'">0</button>
    <button style="color:lightgreen" v-on:click="check_answer">✓</button></p>
    <p><button style="color:lightskyblue" v-on:click="n">Next Question</button></p>
    <p>{{ message }}</p>
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
      symbol : "+"
    },
    methods : {
      d : function () { this.myAnswer = this.myAnswer.slice(0, -1); },
  
      check_answer : function () {
          if (this.answer == parseInt(this.myAnswer, null)) {   
              this.message = "Correct";
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
