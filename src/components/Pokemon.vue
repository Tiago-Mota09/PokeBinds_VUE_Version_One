<template>
  <div id="card" class="card">
    <div class="card-image">
      <figure>
        <img :src="currentImg" alt="Placeholder image">
      </figure>
    </div>
    <div class="card-content">
      <div class="media">
        <div class="media-content">
          <p class="title is-4">{{ index }}. {{ name | upperCase }}</p>
          <p class="subtitle is-6">{{ pokemon.type }}</p>
        </div>
      </div>
      <div class="content">
        <button class="button is-medium is-fullwidth" @click="changeSprite">Mudar Sprite</button>
      </div>
    </div>
    
  </div>
</template>

<script>
import api from '../services/api';

export default {
  name: 'Pokemon',
  props: {
    index: Number,
    name: String,
    url: String
  },
  created: function() {
    api.get(this.url).then((response) => {
      this.pokemon.type = response.data.types[0].type.name;
      this.pokemon.front = response.data.sprites.front_default;
      this.pokemon.back = response.data.sprites.back_default;
      this.currentImg = response.data.sprites.front_default;

    });
  },
  data() {
    return {
      isFront: true,
      currentImg: '',
      pokemon: {
        type: '',
        front: '',
        back: '',
      }
    }
  },
  methods: {
    changeSprite: function() {
      if(this.isFront) {
        this.isFront = false;
        this.currentImg = this.pokemon.back;
      } else {
        this.isFront = true;
        this.currentImg = this.pokemon.front;
      }
    }
  },
 
  filters: {
    upperCase: function(value) {
      var newName = value[0].toUpperCase() + value.slice(1);
      return newName;
    }
  }
}


</script>

<style>
  .card {
    margin: 1vh;
  }

  #card {
    width: 20rem;
  }
/* ====================================================== */
*{
  margin: 0px;
  padding: 0px;
  box-sizing: border-box;
}
html, body, footer {
  background: #EFEFBB;
  background: linear-gradient(to right, rgb(197, 230, 236), rgb(239, 187, 230));
  margin: 0;
  font-family: rubik;
}
  .steel {
  background-color: #f4f4f4;
}

.fire {
  background-color: #FDDFDF;
}

.grass {
  background-color: #DEFDE0;
}

.electric {
  background-color: #FCF7DE;
}

.water, .ice {
  background-color: #DEF3FD;
}

.ground {
  background-color: #f4e7da;
}

.rock {
  background-color: #d5d5d4;
}

.fairy {
  background-color: #fceaff;
}

.poison {
  background-color: #c4add6;
}

.bug {
  background-color: #f8d5a3;
}

.dragon {
  background-color: #97b3e6;
}

.psychic {
  background-color: #eaeda1;
}

.flying {
  background-color: #F5F5F5;
}

.fighting {
  background-color: #E6E0D4;
}

.ghost {
  background-color: #ebc2c2;
}

.normal {
  background-color: #F5F5F5;
}
.footer{
  color: rgb(179, 94, 94);
}
</style>

