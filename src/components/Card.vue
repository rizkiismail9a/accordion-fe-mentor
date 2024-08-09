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
        <li
          @click="showAnswer(!answerShown[q.id], q.id)"
          v-for="q in question"
          :key="q.id"
        >
          <div class="question">
            <span>{{ q.question }}</span>
            <img v-if="!answerShown[q.id]" src="/images/icon-plus.svg" alt="" />
            <img v-if="answerShown[q.id]" src="/images/icon-minus.svg" alt="" />
          </div>
          <Transition name="answer">
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
hr {
  opacity: 0.5;
}

.card-container {
  background-color: white;
  width: 300px;
  margin: auto;
  padding: 12px;
  display: flex;
  flex-direction: column;
  gap: 16px;
  border-radius: 8px;
  box-shadow: 1px 1px 20px rgba(128, 128, 128, 0.212);
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
  cursor: pointer;
  /* border-bottom: 1px solid var(--grayishPurple); */
}

.question:hover {
  color: #ad28eb;
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

.answer-enter-active,
.answer-leave-active {
  transform: translateY(0);
  opacity: 1;
  transition: all 0.4s ease;
}

.answer-enter-from,
.answer-leave-to {
  transform: translateY(-100px);
  opacity: 0;
}

@media screen and (min-width: 768px) {
  .card-container {
    width: 500px;
    padding: 24px;
  }

  .card-header {
    display: flex;
    gap: 12px;
    align-items: center;
  }

  .card-header img {
    width: 36px;
  }

  h1 {
    font-size: 36px;
    font-weight: 700;
  }

  .question {
    display: flex;
    justify-content: space-between;
    align-items: center;
    font-weight: 600;
  }

  .question > span {
    max-width: 410px;
  }

  .question > img {
    width: 24px;
  }

  .answer {
    padding: 12px 0;
  }
}
</style>
