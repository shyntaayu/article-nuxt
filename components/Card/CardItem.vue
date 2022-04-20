<template>
  <div class="col">
    <div class="card shadow-sm">
      <img :src="article.img" class="bd-placeholder-img card-img-top" />
      <div class="card-body">
        <h2>{{ article.title }}</h2>
        <p class="card-text">
          {{ article.content }}
        </p>
        <div class="d-flex justify-content-between align-items-center">
          <div class="btn-group">
            <button type="button" class="btn btn-sm btn-outline-secondary">
              View
            </button>
            <button type="button" class="btn btn-sm btn-outline-secondary">
              Edit
            </button>
          </div>
          <small class="text-muted">9 mins</small>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    article: {
      type: Object,
      default: {
        title: "Untitled",
        content: " Undescribe",
        img: "",
      },
    },
  },
};
</script>
