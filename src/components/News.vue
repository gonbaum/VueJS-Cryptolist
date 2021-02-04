<template>
  <section class="section">
    <main class="container">
      <div class="box" v-for="item in news" :key="item.key">
        <div class="card">
          <div class="card-image">
            <figure class="image is-4by3">
              <img v-bind:src="item.imageurl" alt="" />
            </figure>
          </div>
          <div class="card-content">
            <div class="media">
              <div class="media-content">
                <a
                  class="title is-link"
                  v-bind:href="item.guid"
                  target="_blank"
                  >{{ item.title }}</a
                >
              </div>
            </div>
            <div class="content">
              {{ item.body }}
              <br />
              <br />
              
            </div>
            <nav class="level is-mobile">
                <div class="level-left">
                  <div class="field is-grouped is-grouped-multiline">
                    <div class="control">
                      <div class="level-item tags has-addons">
                        <span class="tag"
                          ><i class="fas fa-thumbs-up"></i
                        ></span>
                        <span class="tag is-link">{{ item.upvotes }}</span>
                      </div>
                    </div>
                    <div class="control">
                      <div class="level-item tags has-addons">
                        <span class="tag"
                          ><i class="fas fa-thumbs-down"></i
                        ></span>
                        <span class="tag is-link">{{ item.downvotes }}</span>
                      </div>
                    </div>
                  </div>
                </div>
                <div class="level-right">
                  <div class="level-item tags has-addons">
                    <span class="tag"><i>source</i></span>
                    <span class="tag is-primary">{{ item.source }}</span>
                  </div>
                </div>
              </nav>
          </div>
        </div>
      </div>
    </main>
  </section>
</template>

<script>
import axios from "axios";
export default {
  name: "news",
  data: () => ({
    news: [],
    errors: [],
  }),
  created() {
    axios
      .get("https://min-api.cryptocompare.com/data/v2/news/?lang=EN")
      .then((response) => {
        this.news = response.data.Data;
        console.log(response.data.Message);
      })
      .catch((e) => {
        this.errors.push(e);
      });
  },
};
</script>

<style scoped>
a.title:hover {
  color: #3273dc;
}

.container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(500px, 1fr));
}

.card {
  height: 100%;
  display: flex;
  flex-direction: column;
  height: 100%;
}

.card-content {
  display: flex;
  flex-direction: column;
  /* height: fit-content; */
  height: 100%;
  justify-content: space-between;
}
</style>
