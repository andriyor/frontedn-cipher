<template>
  <v-app>
    <v-toolbar app>
      <v-toolbar-title class="headline text-uppercase">
        <span class="font-weight-light">Шифрування тексту</span>
      </v-toolbar-title>
    </v-toolbar>

    <v-content>
      <v-container grid-list-md text-xs-center>
        <v-layout row wrap>
          <v-flex xs4>
            <v-btn color="success">button1</v-btn>
          </v-flex>
          <v-flex xs4>
            <v-btn color="success">Обернути
              <v-icon right dark>compare_arrows</v-icon>
            </v-btn>
          </v-flex>
          <v-flex xs4>
            <v-btn color="success">button2</v-btn>
          </v-flex>
        </v-layout>

        <v-layout row wrap>
          <v-flex xs6>
            <v-textarea
              name="input-7-1"
              label="Input"
              value=""
              v-model="input"
              hint="input"
            ></v-textarea>
          </v-flex>
          <v-flex xs6>
            <v-textarea
              name="input-7-1"
              label="Output"
              value=""
              v-model="output"
              hint="output"
            ></v-textarea>
          </v-flex>
        </v-layout>

        <v-layout row wrap>
          <v-flex xs4>
            <v-select
                    :items="items"
                    label="Оберіть шифр"
            ></v-select>
            <v-container fluid>
              <p>Дія</p>
              <v-radio-group v-model="radios" :mandatory="false">
                <v-radio label="Шифрувати" value="radio-1"></v-radio>
                <v-radio label="Розшифрувати" value="radio-2"></v-radio>
              </v-radio-group>
            </v-container>

          </v-flex>

          <v-flex xs4>
            <v-checkbox v-model="checkbox" label="Завжди очищати результат"></v-checkbox>
            <div>
              <v-btn color="success" v-on:click="greet">Застосувати
                <v-icon right dark>arrow_right_alt</v-icon>
              </v-btn>
            </div>
            <div>
              <v-btn color="success">Вихід
                <v-icon right dark>exit_to_app</v-icon>
              </v-btn>
            </div>
          </v-flex>

          <v-flex xs4>
            <v-btn flat icon color="indigo">
              <v-icon right dark>folder</v-icon>
            </v-btn>
            <v-btn flat icon color="indigo">
              <v-icon right dark>save_alt</v-icon>
            </v-btn>
            <div>
              <v-btn color="success">Відкрити з файлу
                <v-icon right dark>attachment</v-icon>
              </v-btn>
            </div>
            <div>
              <v-btn color="success">зберегти результат в файл
                <v-icon right dark>save</v-icon>
              </v-btn>
            </div>
          </v-flex>
        </v-layout>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
// import HelloWorld from './components/HelloWorld'

export default {
  name: 'App',
  components: {

  },
  data: () => ({
    items: ['Абаш', 'Цезаря'],
    radios: 'radio-1',
    input: '',
    output: '',
    checkbox: true,
  }),
  methods: {
    greet() {
      fetch(`atbash?text=${this.input}`)
        .then(function(response) {
          const json = response.json();
          return  this.output = json.name;
        })
        .catch(err => console.error(err));
    }
  }
}
</script>
