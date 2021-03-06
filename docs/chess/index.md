---

title: Chess score

---

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
The following equations from [here](https://en.wikipedia.org/wiki/Elo_rating_system) are used

{% raw %}
<p>$$E_A = \frac{1}{1 + 10^{(R_A - R_B)/400}}$$</p>
<p>$$ R_A^\prime=R_A+K(S_A-E_A $$</p>
{% endraw %}


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
