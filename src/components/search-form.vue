<template>
  <div class="search-form">
    <form
      @submit.prevent="submitHandler"
      class="search-form-wrapper"
    >
      <fieldset
        class="search-form__field"
        :class="{ 'search-form__field_margin': isShowAddSettings }"
      >
        <template v-if="!isNameSearch">
          <div
            v-for="items in mockData.basicSearch"
            :key="items.id"
            class="row"
          >
            <label :for="items.key" />
            <select
              v-model="form[items.key]"
              class="search-form__item"
              :id="items.key"
            >
              <option
                v-for="item in items.list"
                :key="item.id"
                :label="item.label"
                :value="item.id"
              />
            </select>
          </div>
        </template>
        <div
          class="row"
          v-else
        >
          <label for="search" />
          <input
            class="search-form__item"
            v-model="form.nameSearch"
            placeholder="Введите название объекта (бизнес центра, торгового центра, новостройки, логопарка)"
            type="text"
            id="search"
            name="name search"
          >
        </div>
        <button
          class="btn btn-submit"
          type="submit"
        >
          Найти
        </button>
      </fieldset>

      <fieldset
        v-if="isShowAddSettings"
        class="search-form__field"
      >
        <div
          v-if="isPayment"
          class="search-form__price"
        >
          <label for="priceStart" />
          <input
            v-model="form.priceStart"
            class="search-form__item"
            type="text"
            placeholder="От"
            id="priceStart"
            name="price start"
          >
          <label for="priceEnd" />
          <input
            v-model="form.priceEnd"
            class="search-form__item"
            type="text"
            placeholder="До"
            id="priceEnd"
            name="price end"
          >
          <label for="payment"></label>
          <select
            v-model="form.paymentForPeriod"
            class="search-form__item"
            id="payment"
          >
            <option
              v-for="type in mockData.price"
              :key="type.id"
              :label="type.label"
              :value="type.id"
            />
          </select>
        </div>
        <div
          v-else
          class="search-form__price"
        >
          <button
            class="search-form__btn"
            @click="showPaymentSettings(isPayment)"
          >
            Добавить цену
          </button>
        </div>

        <div
          v-if="isFootage"
          class="search-form__footage"
        >
          <label for="footageStart" />
          <input
            v-model="form.footageStart"
            class="search-form__item"
            placeholder="От"
            type="text"
            id="footageStart"
            name="footage-start"
          >
          <label for="footageEnd" />
          <input
            v-model="form.footageEnd"
            class="search-form__item"
            placeholder="До"
            type="text"
            id="footageEnd"
            name="footage-end"
          >
          <div class="search-form__amount">
            <var>M<sup>2</sup></var>
          </div>
        </div>
        <div
          v-else
          class="search-form__footage"
        >
          <button
            class="search-form__btn"
            @click="showFootageSettings(isFootage)"
          >
            Добавить метраж
          </button>
        </div>
      </fieldset>
    </form>


    <div class="search-form__footer">
      <div class="search-form__switch">
        <span
          class="search-form__switch_left"
          :class="{ 'is-active': !isNameSearch }"
        >
          Основной поиск
        </span>
        <v-switch
          :type-search="isNameSearch"
          @change-type-search="changeTypeSearch"
        />
        <span
          class="search-form__switch_right"
          :class="{ 'is-active': isNameSearch }"
        >
          Искать по названию
        </span>
      </div>
      <div
        v-if="!isNameSearch"
        class="search-form__toggle"
      >
        <div
          class="search-form__toggle-btn"
          @click="showPaymentSettings(isPayment)"
        >
          <button>
            {{ priceSymbol }}
          </button>
          <span>
            Цена
          </span>
        </div>
        <div
          class="search-form__toggle-btn"
          @click="showFootageSettings(isFootage)"
        >
          <button>
            {{ footageSymbol }}
          </button>
          <span>
            Метраж
          </span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import VSwitch from './UI/v-switch.vue'

import Data from '../mock.json'

export default {
  name: 'search-form',

  components: {
    VSwitch
  },

  data() {
    return {
      isPayment: false,
      isFootage: false,
      isNameSearch: false,
      form: {
        cityId: '1',
        typeOfRealEstate: '1',
        realEstate: '1',
        priceStart: '',
        priceEnd: '',
        paymentForPeriod: '2',
        nameSearch: '',
        footageStart: '',
        footageEnd: '',
      },
    }
  },

  computed: {
    mockData() {
      return Data
    },

    priceSymbol() {
      return this.isFootage && !this.isPayment ? '+' : this.isPayment ? 'X' : ''
    },

    footageSymbol() {
      return this.isPayment && !this.isFootage ? '+' : this.isFootage ? 'X' : ''
    },

    isShowAddSettings() {
      return this.isPayment || this.isFootage
    }
  },

  methods: {
    submitHandler() {
      console.log('event', this.form);
    },

    changeTypeSearch(typeSearch) {
      this.isNameSearch = typeSearch;
    },

    showFootageSettings(isFootage) {
      this.isFootage = !isFootage
    },

    showPaymentSettings(isPayment) {
      this.isPayment = !isPayment
    },
  }
};
</script>

<style>
.search-form {
  margin: 0 auto;
  background-color: #94c7ea;
  max-width: 940px;
}

.search-form-wrapper {
  padding: 36px 20px;
}

.search-form__field {
  display: flex;
  flex: 1 1 auto;
  border-radius: 4px;
  overflow: hidden;
}

.search-form__field_margin {
  margin-bottom: 28px;
}

.search-form__item {
  display: flex;
  flex: 1 1 auto;
  width: 62px;
  height: 50px;
  background-color: #fff;
  padding: 8px;
  border: none;
  font-size: 18px;
  margin-right: 4px;
}

.search-form__item:not(:last-child) {
  margin-right: 4px;
}

.search-form__price {
  display: flex;
  width: 65%;
  margin-right: 20px;
}

.search-form__footage {
  display: flex;
  width: 35%;
}

.search-form__footage .search-form__item:nth-child(4) {
  margin-right: 0;
}

.search-form__amount {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 54px;
  background-color: #b4e4f3;
}

.search-form__btn {
  display: flex;
  justify-content: center;
  align-items: center;
  flex: 1 1 0;
  height: 50px;
  border: 2px solid #416d82;
  font-size: 18px;
  color: #416d82;
  background-color: transparent;
  cursor: pointer;
  border-radius: 4px;
}

.btn-submit {
  width: 128px;
  height: 50px;
  border: none;
  background-color: #3d9967;
  color: #fff;
  font-size: 18px;
  cursor: pointer;
}



/*-----------------------*\
  #Footer form
\*-----------------------*/
.search-form__footer {
  display: flex;
  justify-content: space-between;
  justify-items: center;
  height: 62px;
  background-color: #e3f4fe;
  padding-left: 20px;
}

.search-form__switch {
  display: flex;
  align-items: center;
}

.search-form__switch_left,
.search-form__switch_right {
  color: #adbfc8;
}

.is-active {
  color: #416d82;
}

.search-form__toggle {
  display: flex;
  align-items: center;
  margin-right: 20px;
}

.search-form__toggle-btn {
  display: flex;
  cursor: pointer;
}

.search-form__toggle-btn:first-child {
  margin-right: 8px;
}

.search-form__toggle-btn button {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 18px;
  height: 18px;
  margin-right: 8px;
  border: 2px solid #416d82;
  border-radius: 50%;
  background-color: transparent;
  color: #416d82;
  cursor: pointer;
  font-size: 12px;
}

.search-form__toggle-btn span {
  color: #416d82;
}
</style>
