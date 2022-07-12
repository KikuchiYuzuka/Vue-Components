<template>
    <div class="container">
        <div class="flex">
            <div class="md:w-1/3"></div>
            <div class="md:w-1/3 w-full">
                <form class="p-3">
                    <label class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2" for="grid-password">
                        パスワード
                    </label>
                    <div class="flex flex-wrap items-stretch w-full relative">
                        <input
                            ref="password"
                            type="password"
                            class="w-px flex-1 border h-10 bg-gray-200 text-gray-700 border border-gray-200 rounded rounded-r-none py-3 px-4 focus:outline-none focus:bg-white focus:border-gray-500"
                            placeholder="******************"
                            v-model="password">
                        <div class="flex -mr-px">
                            <button
                                type="button"
                                class="flex items-center leading-normal bg-grey-lighter rounded rounded-l-none border border-l-0 border-grey-light px-3 whitespace-no-wrap text-grey-dark text-sm"
                                v-text="passwordVisibilityText"
                                @click="changePasswordVisibility"></button>
                        </div>
                    </div>
                    <p :class="passwordMessageCss" v-text="passwordMessage"></p>
                </form>
            </div>
        <div class="md:w-1/3"></div>
        </div>
    </div>
</templete>

<script>
export default defineComponent({
  name: "CheckPassword",
  props: {
  },
  data() {
    return {
        password: '',
        showPassword: false
    }
    methods: {
        changePasswordVisibility() {    
            this.showPassword = !this.showPassword;
            this.$refs.password.type = ((this.showPassword)) ? 'text' : 'password';
            this.$refs.password.focus();

        }
    },
    computed: {
        passwordScore() {   
            let score = 0;
            if(this.password.length >= 11) {
                score += 10;    // 長さが11文字以上あるか
            }
            const patterns =  [
                /\d/,           // 数字があるか
                /[a-z]/,        // 小文字のアルファベットがあるか
                /[A-Z]/,        // 大文字のアルファベットがあるか
                /[^a-zA-Z0-9]/  // 数字・アルファベット以外の文字
            ];
            patterns.forEach((pattern) => {
                if(this.password.match(pattern)) {
                    score += 10;
                }
            });
            return score;
        },
        passwordMessage() {

            let message = '';
            const score = this.passwordScore;

            if(score >= 50) {

                message = '非常に強力';

            } else if(score >= 40) {

                message = '強力';

            } else if(score >= 30) {

                message = '普通';

            } else if(score >= 20) {

                message = '脆弱';

            } else if(score >= 10) {

                message = '非常に脆弱';

            }

            return message;

        },
        passwordMessageCss() {

            let css = [
                'text-gray-600',
                'text-xs',
                'italic',
                'p-2',
                'my-2',
                'font-bold',
                'rounded'
            ];
            const score = this.passwordScore;

            if(score >= 50) {

                css.push('bg-green-200');
                css.push('text-green-700');

            } else if(score >= 40) {

                css.push('bg-blue-200');
                css.push('text-blue-700');

            } else if(score >= 30) {

                css.push('bg-orange-200');
                css.push('text-orange-700');

            } else if(score >= 20) {

                css.push('bg-yellow-200');
                css.push('text-yellow-700');

            } else if(score >= 10) {

                css.push('bg-red-200');
                css.push('text-red-700');

            }

            return css;

        },
        passwordVisibilityText() {

            return (this.showPassword) ? '非表示' : '表示';

        }
    })
</script>