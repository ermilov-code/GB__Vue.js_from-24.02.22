<template>
  <div class="hello">
    <h1>{{ msg }}</h1>

    {{ msg.length }}

    <!-- допустим у нас есть некая строка hello - 
    что можно делать в рамках вывода переменной - вы можете спокойно вывести длину {{ msg.length }} - можете делать джоины и преобразования - все что угодно - можно сделать это напрямую - но есть более лакончиынй способ - называется computed
    Чем отличаются metods от computed - (и вотч) -->

    <hr />
    <!-- <button v-on:click="doThat('hello', $event)">Отправить</button>
    <button @click="doThat('hello', $event)">Закрыть</button> -->
    <!-- когда убирается фокус с input - будем проверять наше значение - 
    focus когда что-то принимает - blur -->
    <!-- <input type="text" @blur="onValidate" /> -->

    <!-- в реакте - как сделать реактивным значением -->
    <!-- что такое директива v-model= - связывает значение вашей data с реальным значением input - как только в input поменяется значение в data тоже сразу меняется значение НО! что происходит на самом деле - на самом деле v-model скрывает под собой следующее  -->
    <!-- есть вторая директива которая назфывается вбайнд - она связывает биндит значение из вашего data -->

    <div class="display">
      <input v-model.number="operand1" type="number" />
      <!-- <input v-model.lazy="operand2" type="number" /> -->
      <!-- <input v-model.trim="operand2" type="text" /> -->
      <input v-model.number="operand2" type="number" />

      = {{ result }}
      <!-- чтобы вывести любые данные - будь то props, либо свойство data, либо компьютед computed, метод - вам нужно обернуть это в двойные фигурные скобки и указать название переменной, которую вы хотите вывести в шаблоне template - если вы не привязываете к чемуто - а вам просто надо вывести - через двойные фигурны скорбки {{}} почему? - разработчики так решили
      
      у v-model есть так называемые директивы -  lazy number trim - 
      lazy - ленивая 

      v-model - реактивная - все что вы вводите - она автоматически вам создает все это дело - 
      у вас есть такое понятие как вотч - когда можно подцепиться на изменение - например вы хотите проверять на адреса введенные в input - чтобы каждый раз не делать запросы вы можете сделать v-model.lazy - и как только фокус уйдет - вотч сработает на изменение данных и у вас оно поменяется 

      v-model.trim - обрезает пробелы (полезно для textarea)
      v-model.number - введеная строка будет автоматически приведена к числу 
      
      Эти методы можно использовать цепочкой 
      <input v-model.lazy.number="operand2" type="text" />

      ===
       -->
    </div>
    <!-- /.display -->

    <!-- у нас есть 4 кнопки - напишем через онклик v-on директиву - и посмотрим как можно вызывать методы - мы уже умеем вызывать метод с параметрами - передавать какие-то значения -  -->
    <div class="keyboard">
      <button v-on:click="result = operand1 + operand2">+</button>
      <button @click="result = operand1 - operand2">-</button>
      <button @click="divide(operand1, operand2)">/</button>
      <button @click="multyply">*</button>
    </div>
    <!-- попробовали разные подходы в написании методов -->
    <!-- /.keyboard -->

    <!-- сначала получили это значение - и для того, чтобы динамически менять наше значение нужно = по сути v-model="operand2" под капотом делает :value="operand1" @input="operand1 = $event.target.value - она биндит  -->
    <!-- <input :value="operand1" @input="operand1 = $event.target.value"> -->

    <!-- сделаем пару кнопочек  -->
    <!-- делаем калькулятор -->



    <!-- ДЗ
    - повторить все, что сегодня сделали
    - через директиву v байнд - которые связывают аргументы - вы можете кнопку задизейблить - можно сделать if else пожалуйста - 
    есть такой кейс - на ноль делить нельзя 
    остаток отбрасывать  -->
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: {
      type: String,
      default: "Empty Props",
      required: true /* обязательный параметр или нет */,
    },
  },
  data() {
    return {
      message: "Hello Vue",
      // наши дефолтные значения
      operand1: 0,
      operand2: 0,
      // нужна некая результирующая переменная
      result: 0,
    };
  },
  methods: {
    doThat(str, evnt) {
      console.log("click", str, evnt);
    },
    // сработал метод, который провалидировал наш
    onValidate() {
      console.log("validation true");
    },
    // в рамках компонента у нас создается инстанс? - ко всем значениям компонента вы можете обращаться через this (1:28)
    divide(op1, op2) {
      this.result = op1 / op2;
    },
    // умножение
    // здесь сработает обычная деструктуризация (но деструктуризация ломает реактивность)
    multyply() {
      const { operand1, operand2 } = this;
      this.result = operand1 * operand2;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
