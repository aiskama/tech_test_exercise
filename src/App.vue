<template>
  <div class="form">
    <div class="form-tabs">
      <button @click="activeTab = 1" class="form-tabs__item">Компонент No1</button>
      <button @click="activeTab = 2" class="form-tabs__item">Компонент No2</button>
    </div>
    <div class="form-blocks">
      <MyForm
          v-if="activeTab === 1"
          :fields="formFields"
          :onSubmit="submitHandler"
          :onCancel="cancelHandler"
      />
      <MyForm
          v-if="activeTab === 2"
          :fields="formFieldsSec"
          :onSubmit="submitHandler"
          :onCancel="cancelHandler"
          :formData="formData"
      />
    </div>
  </div>
</template>
<script>
import MyForm from './components/MyForm.vue';

export default {
  components: {
    MyForm,
  },
  data() {
    return {
      formFields: [
        { name: 'manager', type: 'select',placeholder: 'Менеджер',  options: [
            { value: '1', label: 'Менеджер 1' },
            { value: '2', label: 'Менеджер 2' },
            { value: '3', label: 'Менеджер 3' },
          ],
        },
        { name: 'product',type: 'text', placeholder: 'Название продукта' },
        { name: 'link',type: 'text', placeholder: 'Ссылка в jira',comment: 'Ссылка в jira, включая https://', },
        { name: 'domen',placeholder: 'Домен',  type: 'select', options: [
            { value: '1', label: 'Бэк-офис' },
            { value: '2', label: 'Техплатформа' },
            { value: '3', label: 'Офис больших данных' },
            { value: '4', label: 'Цифровой опыт поставщика' },
          ],
        },

      ],
      formFieldsSec: [
        { name: 'worker', type: 'select',placeholder: 'Сотрудник',  options: [
            { value: '1', label: 'Сотрудник 1' },
            { value: '2', label: 'Сотрудник 2' },
            { value: '3', label: 'Сотрудник 3' },
          ],
        },
        { name: 'boss', type: 'select',placeholder: 'Руководитель сотрудника',  options: [
            { value: '1', label: 'Руководитель сотрудника 1' },
            { value: '2', label: 'Руководитель сотрудника 2' },
            { value: '3', label: 'Руководитель сотрудника 3' },
          ],
        },
        { name: 'bet', type: 'select',placeholder: 'Тип ставки',  options: [
            { value: '1', label: 'opex' },
            { value: '2', label: 'capex' },
          ],
        },
        { name: 'unit', type: 'select',placeholder: 'Бизнес-единица ',  options: [
            { value: '1', label: 'MVM' },
            { value: '2', label: 'MTech' },
          ],
        },
        { name: 'product',type: 'number', placeholder: 'Процент капитализации' },
        { name: 'link',type: 'text', placeholder: 'Должность'},
      ],
      activeTab: 1,
    };
  },
  methods: {
    submitHandler(formData) {
      console.log('Отправка данных:', formData);
    },
    cancelHandler() {
      console.log('Отмена');
    },
  },
};
</script>

<style lang="stylus">
.form {
  display flex
  flex-direction column
  gap 30px
  margin 30px
  &-blocks {
    display flex
  }

  &-tabs {
    display flex
    gap 5px
    align-items: center;
    justify-content: center;
    &__item {
      background-color: #8a2be2;
      color: #fff;
      padding: 10px 20px;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      margin-right: 10px;
      font-size: 16px;
    }

    .toggle-button:hover {
      background-color: #6b1a9e;
    }

    .fade-enter-active, .fade-leave-active {
      transition: opacity 0.5s;
    }

    .fade-enter, .fade-leave-to {
      opacity: 0;
    }
  }
}
</style>

