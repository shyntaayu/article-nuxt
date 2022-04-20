<template>
  <div class="py-4">
    <div class="container">
      <div class="title d-flex align-items-center justify-content-between py-2">
        <h5>Article</h5>
        <div class="d-flex align-items-center ms-auto">
          <button
            class="btn btn-outline-primary py-1 px-3 me-4"
            @click="shuffle"
          >
            Shuffle!
          </button>

          <button class="btn btn-success me-4" @click="sortMe">
            Sort {{ isAsc ? "Asc" : "Desc" }}
          </button>

          <!-- /* Form input pencarian */ -->
          <input
            type="text"
            class="form-control"
            placeholder="Search"
            v-model="searchQuery"
          />
        </div>
      </div>

      <transition-group
        name="articles"
        tag="div"
        class="row row-cols-1 row-cols-sm-2 row-cols-md-3 g-3"
      >
        <CardItem
          v-for="(item, i) in resultQuery"
          :key="item.id"
          :article="item"
        />
      </transition-group>
    </div>
  </div>
</template>
<script>
import CardItem from "@/components/Card/CardItem.vue";
export default {
  components: {
    CardItem,
  },
  data() {
    return {
      //var penampung teks pencarian
      searchQuery: "",
      articles: [
        {
          id: 1,
          title: "Judul Artikel 1",
          content:
            "Lorem ipsum dolor sit amet, consectetur adipisicing elit. Placeat dolor explicabo sint quos exercitationem fugiat reiciendis assumenda. Ad quia veritatis, dolor odit, voluptas numquam modi porro eius reprehenderit ullam tenetur?",
          img: "https://images.unsplash.com/photo-1649282806617-c51bb282899c?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=2070&q=80",
        },
        {
          id: 2,
          title: "Judul Artikel 2",
          content:
            "Lorem ipsum dolor sit amet, consectetur adipisicing elit. Placeat dolor explicabo sint quos exercitationem fugiat reiciendis assumenda. Ad quia veritatis, dolor odit, voluptas numquam modi porro eius reprehenderit ullam tenetur?",
          img: "https://images.unsplash.com/photo-1635732646038-0a1a2fe3f2d6?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1074&q=80",
        },
        {
          id: 3,
          title: "Judul Artikel 3",
          content:
            "Lorem ipsum dolor sit amet, consectetur adipisicing elit. Placeat dolor explicabo sint quos exercitationem fugiat reiciendis assumenda. Ad quia veritatis, dolor odit, voluptas numquam modi porro eius reprehenderit ullam tenetur?",
          img: "https://images.unsplash.com/photo-1640006807976-a6127e9d6fa0?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1171&q=80",
        },
      ],
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
  mounted() {},
  created() {
    // if (localStorage.getItem("task-me") != undefined)
    //   this.articles = localStorage.getItem("task-me");
  },
  updated() {
    // localStorage.setItem("task-me", this.articles);
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
