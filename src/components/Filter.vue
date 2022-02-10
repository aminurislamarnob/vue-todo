<template>
    <div class="filter mb-4 pb-4 border-b">
        <div class="filter__left">
          <button class="filter__button" :class="{ 'filter__button--active': selectedFilter == 'all' }" @click="$emit('filterAll')">All ({{ total }})</button>
          <button class="filter__button" :class="{ 'filter__button--active': selectedFilter == 'pending' }" @click="$emit('filterPending')">Pending ({{ pending }})</button>
          <button class="filter__button" :class="{ 'filter__button--active': selectedFilter == 'done' }" @click="$emit('filterDone')">Done ({{ done }})</button>
        </div>
        <div>
          <button class="filter__button filter__button--danger" @click="$emit('clear')">Clear</button>
        </div>
    </div>
</template>

<script>
export default {
    props: ["selectedFilter", "total", "pending", "done"]
}
</script>