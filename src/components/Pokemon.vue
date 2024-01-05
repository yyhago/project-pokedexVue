<template>
  <div>
    <div class="card">
      <div class="card-image">
        <figure>
          <img
            :src="currentImg"
            alt="Placeholder image"
          />
        </figure>
      </div>
      <div class="card-content">
        <div class="media">
          <div class="media-content">
            <p class="title is-4">{{ num }} - {{ formattedName }}</p>
            <p class="subtitle is-6">{{ pokemon.type }}</p>
          </div>
        </div>

        <div class="content">
          <button
            id="btnSprite"
            class="button is-fullwidth"
            @click="mudarSprite"
          >
            Mudar Sprite
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  created: function () {
    axios.get(this.url).then((res) => {
      this.pokemon.type = res.data.types[0].type.name;
      this.pokemon.front = res.data.sprites.front_default;
      this.pokemon.back = res.data.sprites.back_default;
      this.currentImg = this.pokemon.front;
      console.log(this.pokemon);
    });
  },

  data() {
    return {
      isFront: true,
      currentImg: "",
      pokemon: {
        type: "",
        front: "",
        back: "",
      },
    };
  },

  props: {
    num: Number,
    name: String,
    url: String,
  },
  computed: {
    formattedName: function () {
      if (typeof this.name === "string") {
        return this.name[0].toUpperCase() + this.name.slice(1);
      } else {
        console.log("Erro na formatação");
        return this.name;
      }
    },
  },
  methods: {
    mudarSprite: function () {
      if (this.isFront) {
        this.isFront = false;
        this.currentImg = this.pokemon.back;
      } else {
        this.isFront = true;
        this.currentImg = this.pokemon.front;
      }
    },
  },
};
</script>

<style scoped>
.card {
  padding-bottom: 1rem;
  text-align: center;
  margin-top: 2%;
  background-color: #04b2d9;
  box-shadow: 2px 2px 3px 3px #424141;
}

img {
  width: 30%;
  height: 20%;
  display: flex;
  margin: 0 auto;
}

#btnSprite {
  background-color: #011c40;
  color: white;
  border: none;
  border-radius: 7px;
}
</style>
