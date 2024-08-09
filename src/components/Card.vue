<script setup lang="ts">
import { reactive } from "vue";
import question from "../config/question";

const answerShown = reactive<{ [key: number]: boolean }>({
  1: false,
  2: false,
  3: false,
  4: false,
});

/*
 *
 */
const showAnswer = (isShown: boolean, id: number): void => {
  answerShown[id] = isShown;
};
</script>

<template>
  <div class="card-container">
    <div class="card-header">
      <img src="/images/icon-star.svg" alt="icon-star" />
      <h1>FAQs</h1>
    </div>
    <div class="faqs-list">
      <ul>
        <li v-for="q in question" :key="q.id">
          <div class="question">
            <span>{{ q.question }}</span>
            <img
              v-if="!answerShown[q.id]"
              src="/images/icon-plus.svg"
              alt=""
              @click="showAnswer(true, q.id)"
            />
            <img
              v-if="answerShown[q.id]"
              src="/images/icon-minus.svg"
              alt=""
              @click="showAnswer(false, q.id)"
            />
          </div>
          <Transition>
            <div v-show="answerShown[q.id]" class="answer">
              {{ q.answer }}
            </div>
          </Transition>
          <hr v-if="q.id !== question.length" />
        </li>
      </ul>
    </div>
  </div>
</template>

<style scoped>
.card-container {
  background-color: white;
  width: 300px;
  margin: auto;
  padding: 12px;
  display: flex;
  flex-direction: column;
  gap: 16px;
  border-radius: 8px;
}
.card-header {
  display: flex;
  gap: 12px;
  align-items: center;
}
.card-header img {
  width: 18px;
}
h1 {
  font-size: 24px;
  font-weight: 700;
}

ul {
  display: flex;
  flex-direction: column;
  gap: 12px;
}
ul li {
  display: flex;
  flex-direction: column;
  gap: 16px;
  list-style-type: none;
  font-size: 16px;
  color: var(--darkPurple);
  padding: 12px 0px;
  /* border-bottom: 1px solid var(--grayishPurple); */
}
.question {
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-weight: 600;
}
.question > span {
  max-width: 210px;
}
.question > img {
  width: 16px;
  /* flex: 1 1 0%; */
}
.answer {
  padding: 12px 0;
}

.v-enter-active,
.v-leave-active {
  transform: translateY(0);
  opacity: 1;
  transition: all 0.4s ease;
}

.v-enter-from,
.v-leave-to {
  transform: translateY(-100px);
  opacity: 0;
}
</style>
