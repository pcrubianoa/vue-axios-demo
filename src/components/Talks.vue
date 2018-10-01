<template>
  <div class="container">
    <div class="content">
      <h1>Talks</h1>
    </div>
    <div class="columns is-multiline">
      <div :key="talk.id" class="column is-one-quarter-desktop is-one-third-tablet" v-for="talk in talks">
        <div class="b-talk">
          <div class="b-talk__image">
            <img :src="talk.thumbnail | fixImageURL"
                 alt=""/>
          </div>
          <div class="b-talk__title-container">
            <a href="#" class="b-talk__title-link">
              <h2 class="b-talk__title-text">{{talk.title}}</h2>
            </a>
          </div>
          <div class="b-talk__summary">
            {{talk.summary}}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
    import axios from "axios";
    export default {
        name: "Talks",
        data() {
            return {
                talks: []
            };
        },
        mounted() {
            const serviceURL = "http://conference.webtraining.fun/api/talks/";
            axios.get(serviceURL).then(response => {
                this.talks = response.data;
            });
        },
        filters: {
            fixImageURL: function(filePath) {
                const serviceURL = "http://conference.webtraining.fun/";
                if (!filePath) return "";
                return `${serviceURL}${filePath}`;
            }
        }
    };
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  .b-talk {
    overflow: hidden;
  }
  .b-talk__image img {
    max-width: 100%;
    height: auto;
  }
  .b-talk {
    transition: all 0.3s ease-in-out;
    box-shadow: 0 0 2rem rgba(0, 0, 255, 0.1);
    border-radius: 1rem;
  }
  .b-talk:hover {
    -webkit-transform: translateY(-5px);
    transform: translateY(-5px);
    box-shadow: 0 0 10px 0 rgba(0, 0, 0, 0.1);
  }
  .b-talk__title-link {
    color: #000;
  }
  .b-talk__title-text {
    color: #000;
    padding: 10px 20px;
    font-size: 1.4em;
    font-weight: bold;
  }
  .b-talk__title-link:hover {
    color: #23d160;
  }
  .b-talk__summary {
    line-height: 1.5;
    padding: 0 20px 30px 20px;
  }
</style>