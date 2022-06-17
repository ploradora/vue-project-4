<template>
  <article>
    <p>
      ADVICE #<span> {{ number }} </span>
    </p>
    <q>{{ advice }}</q>
    <img
      class="divider"
      src="../assets/images/pattern-divider-desktop.svg"
      alt="pattern divider"
    />
    <div class="dice-container" @click="getAdvice">
      <img
        class="dice"
        src="../assets/images/icon-dice.svg"
        alt="dice illustration"
      />
    </div>
  </article>
</template>

<script>
export default {
  data() {
    return {
      number: 117,
      advice: "It is easy to sit up and take notice, what's difficult is getting up and taking action.",
    };
  },
  methods: {
    getAdvice() {
      fetch("https://api.adviceslip.com/advice")
        .then((res) => res.json())
        .then((data) => {
          const dataId = data.slip.id;
          const dataAdvice = data.slip.advice;
          this.number = dataId;
          this.advice = dataAdvice;
        });
    },
  },
};
</script>

<style scoped lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Manrope:wght@800&display=swap");
article {
  position: relative;
  width: 90%;
  max-width: 400px;
  padding: 1.5rem 2rem 0 2rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  border-radius: 10px;
  text-align: center;
  color: #fff;
  background-color: hsl(217, 19%, 24%);
  font-family: "Manrope", sans-serif;
  box-shadow: 0 5px 14px rgba(0,0,0,0.2);
  p {
    letter-spacing: 2px;
    font-size: 0.7rem;
    color: hsl(150, 100%, 66%);
  }
  q {
    margin-top: 1.6rem;
    margin-bottom: 1.5rem;
    font-size: 23px;
    color: hsl(193, 38%, 86%);
  }
  .divider {
    margin-bottom: 3rem;
    width: 100%;
  }
  .dice-container {
    position: absolute;
    bottom: -1.7rem;
    border-radius: 50%;
    background-color: hsl(150, 100%, 66%);
    padding: 1.1rem;
    display: flex;
    cursor: pointer;
    &:hover {
      box-shadow: 0 0 17px hsl(150, 100%, 66%);
    }
    .dice {
      width: 1.2rem;
    }
  }
}
</style>
