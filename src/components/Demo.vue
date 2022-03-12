<template>
  <h1>Demo: vue-use-paginator</h1>

  <form action="" @submit.prevent.stop>
    <div id="inputs">
      <label>
        numButtons:
      </label>
      <input type="number" v-model.number="numButtons">

      <label>
        numItems:
      </label>
      <input type="number" v-model.number="numItems">

      <label>
        pageSize:
      </label>
      <select v-model.number="pageSize">
        <option>5</option>
        <option>10</option>
        <option>25</option>
        <option>50</option>
        <option>100</option>
      </select>

      <label>
        page:
      </label>
      <input type="number" v-model.number="page">
    </div>

    <br>
    <br>

    <div>numPages: {{ numPages }}</div>

    <br>

    <div>slice: {{ slice }}</div>

    <br>

    <div>hasPrev: {{ hasPrev }}</div>
    <div>hasNext: {{ hasNext }}</div>

    <br>

    <label>buttons:</label>
    <ul>
      <li v-for="(button, idx) in buttons" :key="idx">
        {{ button }}
      </li>
    </ul>

    <label>styled:</label>
    <ul class="paginator">
      <li class="control" :class="!hasPrev && 'disabled'" @click="goStart">
        {{ '<<' }}
      </li>
      <li class="control" :class="!hasPrev && 'disabled'" @click="goPrev">
        {{ '<' }}
      </li>
      <li
        v-for="(button, idx) in buttons"
        :key="idx"
        :class="{ 'current-page': button.active }"
        @click="page = button.page"
      >
        {{ button.ellipsis ? '...' : button.page }}
      </li>
      <li class="control" :class="!hasNext && 'disabled'" @click="goNext">
        {{ '>' }}
      </li>
      <li class="control" :class="!hasNext && 'disabled'" @click="goEnd">
        {{ '>>' }}
      </li>
    </ul>

  </form>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import usePaginator from 'vue-use-paginator'

export default defineComponent({
  setup() {
    return usePaginator({
      pageSize: 10,
      numItems: 70,
      numButtons: 5,
    })
  }
})
</script>

<style scoped>
#inputs {
  display: inline-grid;
  grid-template-columns: 1fr 1fr;
  column-gap: 1rem;
}
#inputs input, #inputs select {
  box-sizing: border-box;
  width: 60px;
}

ul.paginator {
  display: flex;
  list-style: none;
  user-select: none;
}
ul.paginator li {
  display: flex;
  justify-content: center;
  align-items: center;
  box-sizing: border-box;
  width: 50px;
  height: 50px;
  border: 1px solid black;
}
ul.paginator li:not(.current-page):hover {
  font-weight: bold;
  border-width: 2px;
  cursor: pointer;
}
ul.paginator li.current-page {
  color: blue;
  border-color: blue;
}
ul.paginator li.control {
  border: none;
  font-weight: 900;
  cursor: pointer;
}
ul.paginator li.control.disabled {
  opacity: 0.5;
  pointer-events: none;
}
</style>