<template>
  <div id="app">
    <form class="form" @submit.prevent="submit">
      <div class="form-content">
        <div class="form__main">
          <div class="form__main-conteiner">
            <label for="surname">Фамилия*</label>
            <input
              id="surname"
              type="text"
              :class="$v.surname.$error ? 'is-invalid' : ''"
              v-model.trim="surname"
            />
            <p
              class="error-message"
              v-if="$v.surname.$dirty && !$v.surname.required"
            >
              {{ error_message }}
            </p>
          </div>
          <div class="form__main-conteiner">
            <label for="name">Имя*</label>
            <input
              id="name"
              type="text"
              :class="$v.name.$error ? 'is-invalid' : ''"
              v-model.trim="name"
            />
            <p class="error-message" v-if="$v.name.$dirty && !$v.name.required">
              {{ error_message }}
            </p>
          </div>
          <div class="form__main-conteiner">
            <label for="patronymic">Отчество</label>
            <input id="patronymic" type="text" />
          </div>
          <div class="form__main-conteiner">
            <label for="birthday">Дата рождения*</label>
            <input
              id="birthday"
              type="date"
              :class="$v.birthday.$error ? 'is-invalid' : ''"
              v-model.trim="birthday"
            />
            <p
              class="error-message"
              v-if="$v.birthday.$dirty && !$v.birthday.required"
            >
              {{ error_message }}
            </p>
          </div>
          <div class="form__main-conteiner">
            <label for="telephone">Номер телефона*</label>
            <input
              id="telephone"
              type="number"
              :class="$v.telephone.$error ? 'is-invalid' : ''"
              v-model.trim="telephone"
            />
            <p
              class="error-message"
              v-if="$v.telephone.$dirty && !$v.telephone.required"
            >
              {{ error_message }}
            </p>
            <p
              class="error-message"
              v-if="$v.telephone.$dirty && !$v.telephone.minLength"
            >
              Должно быть больше 11 цифр
            </p>
            <p
              class="error-message"
              v-if="$v.telephone.$dirty && !$v.telephone.maxLength"
            >
              Должно быть меньше 12 цифр
            </p>
            <p
              class="error-message"
              v-if="$v.telephone.$dirty && !$v.telephone.notSeven"
            >
              Не 7
            </p>
          </div>
          <div class="form__main-select">
            <div class="main-select__item">
              <label for="sex">Пол</label>
              <select id="sex">
                <option selected hidden>Не указан</option>
                <option value="">Мужской</option>
                <option value="">Женский</option>
              </select>
            </div>
            <div class="main-select__item">
              <label for="group-clients">Группа клиентов*</label>
              <select
                class="group-clients"
                size="3"
                multiple
                :class="$v.groups.$error ? 'is-invalid' : ''"
                v-model="groups"
              >
                <option v-for="(client, index) in group_client" :key="index">
                  {{ client }}
                </option>
              </select>
              <p
                class="error-message"
                v-if="$v.groups.$dirty && !$v.groups.group"
              >
                {{ error_message }}
              </p>
            </div>

            <div class="main-select__item">
              <label for="doctor">Лечащий врач</label>
              <select name="" id="doctor">
                <option value="">Иванов</option>
                <option value="">Захаров</option>
                <option value="">Чернышева</option>
              </select>
            </div>
          </div>
          <div class="form__main-checkbox">
            <label for="send_SMS">Не отправлять СМС</label>
            <input type="checkbox" id="send_SMS" class="send_SMS" />
          </div>
        </div>
        <div class="form__address">
          <h3>Адрес</h3>
          <div class="form__adress-container">
            <div class="adress-container__item">
              <label for="index">Индекс</label>
              <input id="index" type="text" />
            </div>
            <div class="adress-container__item">
              <label for="country">Страна</label>
              <input id="country" type="text" />
            </div>
          </div>
          <div class="form__adress-container">
            <div class="adress-container__item">
              <label for="region">Область</label>
              <input id="region" type="text" />
            </div>
            <div class="adress-container__item">
              <label for="city">Город*</label>
              <input
                id="city"
                type="text"
                :class="$v.city.$error ? 'is-invalid' : ''"
                v-model.trim="city"
              />
              <p
                class="error-message"
                v-if="$v.city.$dirty && !$v.city.required"
              >
                {{ error_message }}
              </p>
            </div>
          </div>
          <div class="form__adress-container">
            <div class="adress-container__item">
              <label for="street">Улица</label>
              <input id="street" type="text" />
            </div>
            <div class="adress-container__item">
              <label for="house">Дом</label>
              <input id="house" type="text" />
            </div>
          </div>
        </div>
        <div class="form__passport">
          <h3>Паспорт</h3>
          <div class="form__passport-conteiner">
            <div class="passport-conteiner__item">
              <label for="type-document">Тип документа*</label>
              <select
                id="type-document"
                :class="$v.documents.$error ? 'is-invalid' : ''"
                v-model.trim="documents"
              >
                <option v-for="(type, index) in type_document" :key="index">
                  {{ type }}
                </option>
              </select>
              <p
                class="error-message"
                v-if="$v.documents.$dirty && !$v.documents.required"
              >
                {{ error_message }}
              </p>
            </div>
            <div class="passport-conteiner__item">
              <label for="series">Серия</label>
              <input id="series" type="text" />
            </div>
          </div>
          <div class="form__passport-conteiner">
            <div class="passport-conteiner__item">
              <label for="number">Номер</label>
              <input id="number" type="text" />
            </div>
            <div class="passport-conteiner__item">
              <label for="who-give">Кем выдан</label>
              <input id="who-give" type="text" />
            </div>
          </div>
          <div class="passport-conteiner__date">
            <label for="date-give">Дата выдачи*</label>
            <input
              id="date-give"
              type="date"
              :class="$v.issue_data.$error ? 'is-invalid' : ''"
              v-model.trim="issue_data"
            />
            <p
              class="error-message"
              v-if="$v.issue_data.$dirty && !$v.issue_data.required"
            >
              {{ error_message }}
            </p>
          </div>
        </div>
        <button type="submit" class="button__add">Отправить</button>
      </div>
    </form>
  </div>
</template>

<script>
import { required, minLength, maxLength } from "vuelidate/lib/validators";
export default {
  name: "App",
  data() {
    return {
      surname: "",
      name: "",
      birthday: "",
      telephone: "",
      group_client: ["VIP", "Проблемный", "ОМС"],
      groups: [],
      city: "",
      type_document: [
        "Паспорт",
        "Свидетельство о рождении",
        "Вод. удостоверение",
      ],
      documents: [],
      issue_data: "",
      error_message: "Это обязательное поле",
    };
  },
  validations: {
    surname: { required },
    name: { required },
    birthday: { required },
    telephone: {
      required,
      minLength: minLength(11),
      maxLength: maxLength(11),
      notSeven(telephone) {
        return telephone[0] == 7;
      },
    },
    groups: {
      group(value) {
        return value.length >= 1;
      },
    },
    documents: { required },
    city: { required },
    issue_data: { required },
  },
  methods: {
    submit() {
      this.$v.$touch();
      if (this.$v.$error) {
        alert("валидация не пройдена");
      } else {
        alert("Новый клиент успешно создан!");
      }
    },
  },
};
</script>

<style lang="scss">
@import "./styles.scss";
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.is-invalid {
  border: 1px solid red;
}
.error-message {
  color: red;
  margin: 0;
}
</style>
