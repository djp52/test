---

title: Chess score

---
<!-- KATEX math rendering -->
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/KaTeX/0.7.1/katex.min.css">
<script src="https://cdnjs.cloudflare.com/ajax/libs/KaTeX/0.7.1/katex.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/KaTeX/0.7.1/contrib/auto-render.min.js"></script>

<!-- VUE -->
<script src="https://cdn.jsdelivr.net/npm/vue@2"></script>

# Chess

Calculates updated chess ratings using the ELO calculation.

{% raw %}
<div id="app-chess">
  <input type="number" v-model="s1" v-on:input="calculate_scores"/>
  <input type="number" v-model="s2" v-on:input="calculate_scores"/>
  <input type="number" v-model="K" v-on:input="calculate_scores"/>
  
  <p>E<sub>A</sub> = {{ 100 * Ea.toFixed(2) }}%</p>
  <table>
      <tr><th>Result</th><th>Delta</th><th>New Score</th></tr>
      <tr><td>Win</td><td>{{ dwin.toFixed(0) }}</td><td>{{ twin.toFixed(0) }}</td></tr>
      <tr><td>Draw</td><td>{{ ddraw.toFixed(0) }}</td><td>{{ tdraw.toFixed(0) }}</td></tr>
      <tr><td>Lose</td><td>{{ dlose.toFixed(0) }}</td><td>{{ tlose.toFixed(0) }}</td></tr>
  </table>
  
</div>

{% endraw %}

<p>$$E=mc^2$$</p>

<script>

var chess_score = new Vue ({
  el: '#app-chess',
  data: {
      s1 : 1200,
      s2: 1200,
      
      dwin : 16,
      ddraw : 0,
      dlose : -16,
      
      twin : 1216,
      tdraw : 1200,
      tlose : 1184,
      
      Ea : 0.5,
      K : 32
  },
  
  methods : {
    calculate_scores : function () {
      this.s1 = parseFloat(this.s1);
      this.s2 = parseFloat(this.s2);
      this.Ea = 1.0 / ( 1 + 10 ** ((this.s2 - this.s1)/400.0));
      
      this.dwin = this.K * (1 - this.Ea);
      this.twin = this.s1 + this.dwin;
      
      this.ddraw = this.K * (0.5 - this.Ea);
      this.tdraw = this.s1 + this.ddraw;
      
      this.dlose = this.K * (0 - this.Ea);
      this.tlose = this.s1 + this.dlose;
    }
  }

})


</script>

<script>
        renderMathInElement(document.body);
</script>
