<template>
  <div>
  <!-- Input Card -->
  <div class="card">
    <div class="card-content">
      <div class="content">
        <!-- First Name -->
        <div class="field">
          <label class="label">First Name</label>
          <div class="control">
            <input class="input" type="text" placeholder="Roberta" v-model="firstName">
          </div>
        </div>
        <!-- Favorite Color -->
        <div class="field">
          <label class="label">Favorite Color</label>
          <div class="control">
            <div class="select">
              <select v-model="favoriteColor">
                <option v-for="color in colors" :key="color" v-bind:value="color">{{color}}</option>
              </select>
            </div>
          </div>
        </div>
        <!-- Do you like pizza? -->
        <div class="field">
          <label class="label">Do you like pizza?</label>
          <div class="control">
            <label class="radio">
              <input type="radio" value="1" v-model="likePizza">
              Yes
            </label>
            <label class="radio">
              <input type="radio" value="0" v-model="likePizza">
              No
            </label>
          </div>
        </div>
        <!-- Favorite topping -->
        <div v-if="likePizza == 1" class="field">
          <label class="label">Favorite topping</label>
          <div class="control">
            <label class="radio" v-for="favoriteToppingOpt in favoriteToppingOpts" :key="favoriteToppingOpt" >
            <input type="radio" v-bind:value="favoriteToppingOpt" v-model="favoriteTopping">
              {{ favoriteToppingOpt }}
            </label>
          </div>
        </div>
        <!-- Why don’t you like pizza?  -->
        <div v-if="likePizza == 0" class="field">
          <label class="label">Why don’t you like pizza?</label>
          <div class="control">
            <input class="input" type="text" placeholder="My soul is dead" v-model="whyNoLikePizza">
          </div>
        </div>
      </div>
    </div>
  </div>
  <!-- Form results card -->
  <div class="card">
    <div class="card-content">
      <div class="content">
        <p v-if="!this.noContent">
        Hey, {{firstName}}, I also like <span v-bind:style="{ color: colorCode}">{{favoriteColor}}</span>. I’m <span v-if="likePizza == 1">glad</span><span v-if="likePizza == 0">sad</span> that you <span v-if="likePizza == 1">do</span><span v-if="likePizza == 0">don't</span> like Pizza
<span v-if="likePizza == 1">because I like {{favoriteTopping}} too.</span>
<span v-if="likePizza == 0">, it’s my favorite food. You said: <span class="is-italic">"{{whyNoLikePizza}}"</span>, but I don’t agree. Pizza is awesome.</span>
        </p>
        <p v-else>
          Please fill out the form
        </p>
      </div>
    </div>
  </div>
  </div>
</template>

<script>
export default {
  name: 'PizzaForm',
  data: function() {
    return {
      firstName:'',
      favoriteColor:'',
      likePizza:-1,
      favoriteTopping:'',
      whyNoLikePizza:'',
      colors:['Blue', 'Coquelicot', 'Purple', 'Celadon', 'Viridian', 'Phlox', 'Feldgrau', 'Green'],
      favoriteToppingOpts:['Salami', 'Mushrooms', 'Black Olives', 'Elote', 'Chicken', '24-Karat Gold Leaves', 'Shredded Parmesan Asiago', 'Bacon']
    }
  },
  watch: {
    // If the answer to the question changes, reset the answer to the subquestion
    likePizza: function (val) {
      if(val==1){
        this.whyNoLikePizza = '';
      }else{
        this.favoriteTopping = '';
      }
    }
  },
  computed: {
    // The spec requires the html color code.  This computed property provides that.
    colorCode: function () {
      if(this.favoriteColor == "Blue"){
        return '#0000FF';
      }
      if(this.favoriteColor == "Coquelicot"){
        return '#ff3800';
      }
      if(this.favoriteColor == "Purple"){
        return '#800080';
      }
      if(this.favoriteColor == "Celadon"){
        return '#ACE1AF';
      }
      if(this.favoriteColor == "Viridian"){
        return '#40826d';
      }
      if(this.favoriteColor == "Phlox"){
        return '#df00ff';
      }
      if(this.favoriteColor == "Feldgrau"){
        return '#4d5d53';
      }
      if(this.favoriteColor == "Green"){
        return '#00FF00';
      }
      return '#000000';
    },
    // It would be silly to show the paragraph if no answers are known, yet.
    noContent: function(){
      if(this.firstName == '' && this.favoriteColor == '' && this.likePizza == -1 && this.favoriteTopping == '' && this.whyNoLikePizza == '')
        return true;
      else
        return false;
    }
  }
}
</script>

<style scoped>
	.card{
		margin:10px;
	}
</style>
