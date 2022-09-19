<template>
    <base-card class="text-center">
      <h2>Find Your dev reaper</h2>
      <div class="flex">
        <span class="filter-option">
          <input type="checkbox" id="frontend" checked @change="setFilter" />
          <label for="frontend">Frontend</label>
        </span>
        <span class="filter-option">
          <input type="checkbox" id="backend" checked @change="setFilter" />
          <label for="backend">Backend</label>
        </span>
        <span class="filter-option">
          <input type="checkbox" id="career" checked @change="setFilter" />
          <label for="career">Career</label>
        </span>
      </div>
    </base-card>
</template>

<script>
export default {
  emits: ['change-filter'],
  data() {
    return {
      filters: {
        frontend: true,
        backend: true,
        career: true,
      },
    };
  },
  methods: {
    setFilter(event) {
      const inputId = event.target.id;
      const isActive = event.target.checked;
      const updatedFilters = {
        ...this.filters,
        [inputId]: isActive,
      };
      this.filters = updatedFilters;
      this.$emit('change-filter', updatedFilters);
    },
  },
};
</script>

<style scoped>
h2 {
  margin: 0.5rem 0;
}
.flex {
  display: flex;
  justify-content: center;
  margin-top: 1rem;
}
.text-center {
  text-align: center;
}

.filter-option {
  margin-right: 1rem;
}

.filter-option label,
.filter-option input {
  vertical-align: middle;
}

.filter-option label {
  margin-left: 0.25rem;
}

.filter-option.active label {
  font-weight: bold;
}
[type="checkbox"] {
  height: 1rem;
  width: 1rem;
}
</style>
