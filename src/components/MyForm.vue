<!-- MyForm.vue -->
<template>
  <form @submit.prevent="handleSubmit" class="form-container">
    <div v-for="field in fields" :key="field.name" >
      <label :for="field.name" class="form-container__label">{{ field.label }}</label>
      <div class="form-container__input">
        <input
            v-if="field.type === 'text' || field.type === 'number'"
            :type="field.type"
            :name="field.name"
            v-model="localFormData[field.name]"
            :placeholder="field.placeholder || ''"
            class="form-input"
        />
        <select
            v-else-if="field.type === 'select'"
            :name="field.name"
            v-model="localFormData[field.name]"
            class="form-select"
        >
          <option
              :value="field.value"
              disabled
              hidden
              style="color: rgba(0, 0, 0, 0.5);"
          >
            {{ field.placeholder || 'Выберите...' }}
          </option>
          <option v-for="option in field.options" :key="option.value" :value="option.value">{{ option.label }}</option>
        </select>
        <div v-if="field.comment" class="form-container__comment">{{ field.comment }}</div>
      </div>
    </div>

    <div class="form-buttons">
      <button type="button" @click="handleCancel" class="cancel-button">Отмена</button>
      <button type="submit" class="submit-button">Отправить</button>
    </div>
  </form>
</template>

<script>
export default {
  props: {
    fields: {
      type: Array,
      required: true,
    },
    onSubmit: {
      type: Function,
      required: true,
    },
    onCancel: {
      type: Function,
      required: true,
    },
    formData: {
      type: Object,
      default: () => ({}),
    },
  },
  data() {
    return {
      localFormData: { ...this.formData },
    };
  },
  methods: {
    handleSubmit() {
      this.onSubmit(this.localFormData);
    },
    handleCancel() {
      this.onCancel();
    },
  },
};
</script>

<style lang="stylus">

.form-container {
  display flex
  flex-direction column
  gap 15px
  max-width: 400px;
  margin: 0 auto;
  width: 100%;
  font-family: 'Roboto', sans-serif;
  background-color: #f9f9f9;
  padding: 20px;
  border-radius: 16px;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);

  &__field {
    margin-bottom: 20px;
  }

  &__label {
    display: block;
    font-weight: bold;
    margin-bottom: 8px;
    color: #555;
  }

  &__input {
    position: relative;
  }

  .form-input,
  .form-select {
    width: 100%;
    padding: 15px;
    box-sizing: border-box;
    border: 2px solid #ccc;
    border-radius: 12px;
    font-size: 16px;
    background-color: #f4f4f4;
    color: #333;
    transition: border-color 0.3s ease, box-shadow 0.3s ease;
  }

  .form-input:focus,
  .form-select:focus {
    border-color: #8a2be2;
    box-shadow: 0 0 8px rgba(138, 43, 226, 0.3);
  }

  .form-select {
    cursor: pointer;
  }


  &__comment {
    margin-top: 5px;
    color: #666;
    font-size: 14px;
  }

  .form-buttons {
    display: flex;
    justify-content: space-between;
    margin-top: 20px;
  }

  .cancel-button,
  .submit-button {
    padding: 15px 30px;
    border: none;
    border-radius: 12px;
    cursor: pointer;
    font-size: 16px;
    font-weight: bold;
    transition: background-color 0.3s ease;
  }

  .cancel-button {
    background-color: #e44d26;
    color: #fff;
  }

  .submit-button {
    background-color: #8a2be2;
    color: #fff;
  }

  .cancel-button:hover,
  .submit-button:hover {
    background-color: #333;
  }
}
</style>
