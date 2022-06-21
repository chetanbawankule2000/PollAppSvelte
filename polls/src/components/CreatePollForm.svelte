<script>
  import Button from "../shared/Button.svelte";
  import { createEventDispatcher } from "svelte";
  import PollStore from "../stores/Pollstore.js";

  const dispatch = createEventDispatcher();
  let formFields = {
    question: "",
    answerA: "",
    answerB: "",
  };
  let errors = { question: "", answerA: "", answerB: "" };

  let valid = false;
  const submitHandler = () => {
    valid = true;
    //validate the question
    if (formFields.question.trim().length < 5) {
      valid = false;
      errors.question = "Question must be at least 5 characters long";
    } else {
      errors.question = "";
    }

    // validate the answerA
    if (formFields.answerA.trim().length < 1) {
      valid = false;
      errors.answerA = "Answer shoud not be empty";
    } else {
      errors.answerA = "";
    }

    // validate the answerB
    if (formFields.answerB.trim().length < 1) {
      valid = false;
      errors.answerB = "Answer shoud not be empty";
    } else {
      errors.answerB = "";
    }

    if (valid) {
      console.log("Form data is valid");
      let poll = {
        ...formFields,
        votesA: 0,
        votesB: 0,
        id: Math.random(),
      };

      PollStore.update((currentPolls) => {
        return [poll, ...currentPolls];
      });

      dispatch("addPoll");
    }
  };
</script>

<form on:submit|preventDefault={submitHandler}>
  <div class="form-fields">
    <label for="question">Poll Questiom</label>
    <input type="text" id="question" bind:value={formFields.question} />
    <div class="error">{errors.question}</div>
  </div>
  <div class="form-fields">
    <label for="answerA">Answer A</label>
    <input type="text" id="answerA" bind:value={formFields.answerA} />
    <div class="error">{errors.answerA}</div>
  </div>
  <div class="form-fields">
    <label for="question">Answer B</label>
    <input type="text" id="answerB" bind:value={formFields.answerB} />
    <div class="error">{errors.answerB}</div>
  </div>
  <Button type="secondary" flat={true}>Add Poll</Button>
</form>

<style>
  form {
    max-width: 400px;
    text-align: center;
    margin: 0 auto;
  }
  .form-fields {
    margin: 18px auto;
  }
  input {
    width: 100%;
    border-radius: 6;
  }
  label {
    margin: 10px auto;
    text-align: left;
  }
  .error {
    font-weight: bold;
    color: #d91b42;
    font-size: 12px;
  }
</style>
