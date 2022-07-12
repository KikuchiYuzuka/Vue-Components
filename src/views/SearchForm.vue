<template>
    <div class="search-form">
        <form @submit="submit()" :action="action" method="get" class="search-form">
          <div class="form-content">
            <div class="w-4/12">
              <label class="label" for="account_id">ID</label>
              <input v-model="account_id" type="text" name="account_id" id="account_id" class="form" placeholder="yamada1234" />
            </div>

            <div class="w-4/12">
              <label class="label" for="name">ID</label>
              <input v-model="name" type="text" name="name" id="name" class="form" placeholder="yamada hanako" />
            </div>

            <div class="w-4/12">
              <label class="label" for="tel">ID</label>
              <input v-model="tel" type="text" name="tel" id="tel" class="form" placeholder="09000000000" />
            </div>
          </div>

          <div class="form-content">
            <div class="w-4/12">
              <label class="label" for="prefecture">都道府県</label>
              <select v-model="prefecture"
                      name="prefecture"
                      id="prefecture"
                      class="form"
              >
                <option v-for="(prefecture, index) in prefectures" :key="index" :value="prefecture.value">
                  {{ prefecture.label }}
                </option>
              </select>
            </div>

            <div class="w-4/12">
              <label class="label" for="status">ステータス</label>
              <select v-model="status"
                      name="status"
                      id="status"
                      class="form"
              >
                <option v-for="(status, index ) in statusMaster" :key="index" :value="status.value">
                  {{ status.label }}
                </option>
              </select>
            </div>

            <div class="w-4/12">
              <label class="label" for="year">登録年</label>
              <select v-model="year"
                      name="year"
                      id="year"
                      class="form"
              >
                <option v-for="(year, index) in years" :key="index" :value="year.value">
                  {{ year.label }}
                </option>
              </select>
            </div>
          </div>
          <div class="button-content">
            <button type='submit' class="button" :disabled="isDisabled">
              検索
            </button>
          </div>
        </form>
    </div>
</template>

<script>
export default {
  name: "SearchForm",
  props: {
  },
  data() {
    return {
      prefecture: [
            {
            label: '北海道',
            value: 1,
            },
            {
            label: '青森',
            value: 2,
            },
            {
            label: '岩手',
            value: 3,
            },
            {
            label: '秋田',
            value: 4,
            },
        ],
        statusMaster: [
            {
            label: '完了',
            value: 1,
            },
            {
            label: '登録済',
            value: 2,
            },
            {
            label: '未登録',
            value: 3,
            },
            {
            label: '仮登録',
            value: 4,
            },
        ],
        years: [
            {
            label: 2022,
            value: 2022,
            },
            {
            label: 2021,
            value: 2021,
            },
            {
            label: 2020,
            value: 2020,
            },
            {
            label: 2019,
            value: 2019,
            },
        ],


    }
  },
  methods: {
    submit() {
      this.isDisabled = true;
      setTimeout(function () {
        this.isDisabled = false;
      }.bind(this), 2000)
    }
  },
  mounted() {
    this.isDisabled = false;
  },
}
</script>

