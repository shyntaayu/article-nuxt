<template>
  <div id="app">
    <Header />
    <main class="container">
      <Hero />
      <div class="row mb-2">
        <CardArticle
          v-for="(article, index) in articles"
          :key="index"
          :article="article"
        />
      </div>
    </main>
  </div>
</template>
<script>
import Header from "@/components/Header.vue";
import Footer from "@/components/Footer.vue";
import CardArticle from "@/components/Card/CardArticle.vue";
import Hero from "@/components/Hero.vue";
export default {
  components: {
    CardArticle,
    Header,
    Footer,
    Hero,
  },
  data() {
    return {
      //var penampung teks pencarian
      searchQuery: "",
      articles: [],
      isAsc: true,
    };
  },
  computed: {
    resultQuery() {
      if (this.searchQuery) {
        return this.articles.filter((i) => {
          return this.searchQuery
            .toLowerCase()
            .split(" ")
            .every((v) => i.title.toLowerCase().includes(v));
        });
      } else {
        console.log(this.articles);
        return this.articles;
      }
    },

    resultCategory() {
      let a = this.articles
        .map((item) => item.category)
        .filter((value, index, self) => self.indexOf(value) === index);
      a.push("Nothing selected");
      console.log(a);
      return a;
    },
  },
  methods: {
    shuffle() {
      this.articles = _.shuffle(this.articles);
    },
    sortMe() {
      if (this.isAsc) {
        this.articles = this.articles.sort((a, b) =>
          a.title > b.title ? 1 : -1
        );
      } else {
        this.articles = this.articles.sort((a, b) =>
          a.title > b.title ? -1 : 1
        );
      }
      this.isAsc = !this.isAsc;
    },
  },
  mounted() {
    console.log("Artikel: ", this.articles);
  },
  created() {
    // if (localStorage.getItem("task-me") != undefined)
    //   this.articles = localStorage.getItem("task-me");
  },
  updated() {
    // localStorage.setItem("task-me", this.articles);
  },

  async fetch() {
    await this.$axios
      .get("v1/cnn-news")
      .then((res) => (this.articles = res.data.data));
  },
};
</script>

<style>
.red {
  color: blue;
}
.articles-move {
  transition: 0.4s;
}
</style>
