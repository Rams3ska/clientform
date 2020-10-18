<template>
  <div id="app">
    <aside class="left-aside"></aside>
    <div class="main-section">
      <div class="container">
        <div class="emp"></div>
        <h1>Создание клиента</h1>
        <hr />
        <div class="content-box">
          <div class="form-group">
            <h3>Основная информация</h3>
            <div class="form-row">
              <TextBox
                :name="'Имя *'"
                :placeholder="'Олег'"
                v-model="client.base.name"
                :error="
                  !$v.client.base.name.required
                    ? 'Поле не может быть пустым'
                    : !$v.client.base.name.correct
                    ? 'Поле может содержать только символы [A-z А-я]'
                    : ''
                "
              />
              <TextBox
                :name="'Фамилия *'"
                :placeholder="'Олегов'"
                v-model="client.base.surname"
                :error="
                  !$v.client.base.surname.required
                    ? 'Поле не может быть пустым'
                    : !$v.client.base.surname.correct
                    ? 'Поле может содержать только символы [A-z А-я]'
                    : ''
                "
              />
              <TextBox
                :name="'Отчество'"
                :placeholder="'Олегович'"
                v-model="client.base.patronymic"
                :error="
                  !$v.client.base.patronymic.correct
                    ? 'Поле может содержать только символы [A-z А-я]'
                    : ''
                "
              />
            </div>
            <div class="form-row">
              <Date
                :name="'Дата рождения *'"
                v-model="client.base.birthday"
                :error="
                  !$v.client.base.birthday.validDate
                    ? 'Указана некорректная дата'
                    : ''
                "
              />
              <TextBox
                :name="'Номер телефона *'"
                :placeholder="'+78887776655'"
                v-model="client.base.phone"
                :error="
                  !$v.client.base.phone.correctLength
                    ? 'Указан некорректный номер'
                    : ''
                "
              />
              <Selector
                :name="'Пол'"
                :options="options.sex"
                :value="client.base.sex"
                @change="client.base.sex = $event"
              />
            </div>
            <div class="form-row">
              <Multiselect
                :name="'Группа *'"
                :options="options.groups"
                v-model="client.base.groups"
                :error="
                  !$v.client.base.groups.minOne
                    ? 'Выберите минимум одну группу'
                    : ''
                "
              />
              <Selector
                :name="'Лечащий врач'"
                :options="options.doctors"
                :value="client.base.doctor"
                @change="client.base.doctor = $event"
              />
            </div>
            <div class="form-container form__checkbox">
              <span class="name">Не отправлять СМС</span>
              <input type="checkbox" v-model="client.base.sendMessage" />
            </div>
          </div>
          <hr />
          <div class="form-group">
            <h3>Адрес</h3>
            <div class="form-row">
              <TextBox
                :name="'Индекс'"
                :placeholder="'101000'"
                v-model="client.adress.index"
                :error="
                  !$v.client.adress.index.numeric
                    ? 'Поле может содержать только цифры'
                    : !$v.client.adress.index.maxLength
                    ? 'Макисмальная длина индекса - 6'
                    : ''
                "
              />
              <TextBox
                :name="'Страна'"
                :placeholder="'Россия'"
                v-model="client.adress.country"
                :error="
                  !$v.client.adress.country.correct
                    ? 'Поле может содержать только символы [А-я]'
                    : ''
                "
              />
              <TextBox
                :name="'Область'"
                :placeholder="'Московская обл.'"
                v-model="client.adress.region"
                :error="
                  !$v.client.adress.region.correct
                    ? 'Поле может содержать только символы [А-я._]'
                    : ''
                "
              />
            </div>
            <div class="form-row">
              <TextBox
                :name="'Город *'"
                :placeholder="'Москва'"
                v-model="client.adress.city"
                :error="
                  !$v.client.adress.city.required
                    ? 'Поле не может быть пустым'
                    : !$v.client.adress.city.correct
                    ? 'Поле может содержать только символы [А-я]'
                    : ''
                "
              />
              <TextBox
                :name="'Улица'"
                :placeholder="'Ленина'"
                v-model="client.adress.street"
                :error="
                  !$v.client.adress.street.correct
                    ? 'Поле может содержать только символы [А-я]'
                    : ''
                "
              />
              <TextBox
                :name="'Дом'"
                :placeholder="'15'"
                v-model="client.adress.house"
                :error="
                  !$v.client.adress.house.numeric
                    ? 'Поле может содержать только цифры'
                    : ''
                "
              />
            </div>
          </div>
          <hr />
          <div class="form-group">
            <h3>Паспорт</h3>
            <div class="form-row">
              <Selector
                :name="'Тип документа *'"
                :options="options.documents"
                :value="client.document.type"
                @change="client.document.type = $event"
                :error="
                  !$v.client.document.type.required
                    ? 'Выберите тип документа'
                    : ''
                "
              />
              <TextBox
                :name="'Серия'"
                :placeholder="'1234'"
                v-model="client.document.serial"
                :error="
                  !$v.client.document.serial.numeric
                    ? 'Поле может содержать только цифры'
                    : ''
                "
              />
              <TextBox
                :name="'Номер'"
                :placeholder="'123456'"
                v-model="client.document.id"
                :error="
                  !$v.client.document.id.numeric
                    ? 'Поле может содержать только цифры'
                    : ''
                "
              />
            </div>
            <div class="form-row">
              <TextBox
                :name="'Кем выдан'"
                :placeholder="'УФМС России по гор. Москва'"
                v-model="client.document.issuer"
                :error="
                  !$v.client.document.issuer.correct
                    ? 'Поле может содержать только символы [А-я._]'
                    : ''
                "
              />
              <Date
                :name="'Дата выдачи *'"
                v-model="client.document.issueDate"
                :error="
                  !$v.client.document.issueDate.validDate
                    ? 'Указана некорректная дата'
                    : ''
                "
              />
            </div>
          </div>
        </div>
        <hr />
        <footer>
          <button @click="submit">СОЗДАТЬ КЛИЕНТА</button>
          <span class="error" ref="submitlog"></span>
        </footer>
        <div class="emp"></div>
      </div>
    </div>
  </div>
</template>

<script>
import {
  required,
  numeric,
  maxLength,
  minLength,
} from "vuelidate/lib/validators";
import Multiselect from "./components/Forms/Multiselect";
import TextBox from "./components/Forms/TextBox";
import Selector from "./components/Forms/Selector";
import Date from "./components/Forms/Date";

export default {
  name: "App",
  data: () => ({
    options: {
      documents: ["Паспорт", "Свидетельство о рождении", "Вод. удостоверение"],
      groups: ["Проблемные", "VIP", "ОМС"],
      sex: ["Не выбрано", "Мужской", "Женский", "Другое"],
      doctors: ["Не выбрано", "Иванов", "Захаров", "Чернышева"],
    },
    client: {
      base: {
        name: "",
        surname: "",
        patronymic: "",
        birthday: "",
        phone: "",
        sendMessage: false,
        sex: "Не выбрано",
        doctor: "Не выбрано",
        groups: [],
      },
      adress: {
        index: "",
        country: "",
        region: "",
        city: "",
        street: "",
        house: "",
      },
      document: {
        type: "",
        serial: "",
        id: "",
        issuer: "",
        issueDate: "",
      },
    },
  }),
  methods: {
    submit() {
      if (this.$v.$invalid)
        this.$refs.submitlog.innerHTML =
          "[Не удалось создать клиента]: Данные формы некорректны!";
      else {
        this.$refs.submitlog.innerHTML = "Клиент успешно создан!";
        this.$refs.submitlog.classList.add("corrected");

        console.log(this.client);

        setTimeout(() => {
          this.$refs.submitlog.innerHTML = "";
          this.$refs.submitlog.classList.remove("corrected");
        }, 2000);
      }
    },
  },
  validations: {
    client: {
      base: {
        name: {
          required,
          correct: (val) => /^[a-zA-Zа-яА-Я]{1,64}$/.test(val),
        },
        surname: {
          required,
          correct: (val) => /^[a-zA-Zа-яА-Я]{1,64}$/.test(val),
        },
        patronymic: {
          correct: (val) => /^[a-zA-Zа-яА-Я]{0,64}$/.test(val),
        },
        groups: {
          minOne: (val) => val.length >= 1,
        },
        birthday: {
          validDate: (val) =>
            /^(19|20)\d\d[- /.](0[1-9]|1[012])[- /.](0[1-9]|[12][0-9]|3[01])$/.test(
              val
            ),
        },
        phone: {
          correctLength: (val) =>
            /^((\+7|7|8)+([0-9]){10})$|\b\d{3}[-.]?\d{3}[-.]?\d{4}/.test(val),
        },
      },
      adress: {
        index: {
          maxLength: maxLength(6),
          numeric,
        },
        country: {
          correct: (val) => /^[а-яА-Я]{0,64}$/.test(val),
        },
        region: {
          correct: (val) => /^[а-яА-Я._ ]{0,64}$/.test(val),
        },
        city: {
          required,
          correct: (val) => /^[а-яА-Я]{0,64}$/.test(val),
        },
        street: {
          correct: (val) => /^[а-яА-Я]{0,64}$/.test(val),
        },
        house: {
          numeric,
          minLength: minLength(0),
        },
      },
      document: {
        type: {
          required,
        },
        serial: {
          numeric,
          minLength: minLength(0),
        },
        id: {
          numeric,
          minLength: minLength(0),
        },
        issuer: {
          correct: (val) => /^[а-яА-Я._ ]{0,64}$/.test(val),
        },
        issueDate: {
          validDate: (val) =>
            /^(19|20)\d\d[- /.](0[1-9]|1[012])[- /.](0[1-9]|[12][0-9]|3[01])$/.test(
              val
            ),
        },
      },
    },
  },
  components: {
    Multiselect,
    TextBox,
    Selector,
    Date,
  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Noto+Sans&display=swap");
@import "assets/index.scss";

.form__checkbox {
  flex-direction: row !important;
  align-items: center;
  justify-content: flex-start;

  margin-top: 10px;

  input[type="checkbox"] {
    width: 18px;
    margin-left: 20px;
  }
}

.corrected {
  color: rgb(91, 214, 91);
}

@media screen and (max-width: 768px) {
  .form__checkbox {
    margin-left: 5px !important;
  }
}
</style>