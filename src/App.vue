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
            <v-btn color="success" v-on:click="cleanInput">Очистити</v-btn>
          </v-flex>
          <v-flex xs4>
            <v-btn color="success" v-on:click="reverse">Обернути
              <v-icon right dark>compare_arrows</v-icon>
            </v-btn>
          </v-flex>
          <v-flex xs4>
            <v-btn color="success" v-on:click="cleanOutput">Очистити</v-btn>
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
                    v-model="celectedCipher"
                    label="Оберіть шифр"
            ></v-select>
            <v-container fluid>
              <div v-if="celectedCipher === items[1].value">
                <v-text-field
                  label="Значення ключа"
                  v-model="key"
                ></v-text-field>
                <p>Дія</p>
                <v-radio-group v-model="radios" :mandatory="false">
                  <v-radio label="Шифрувати" value="true"></v-radio>
                  <v-radio label="Розшифрувати" value="false"></v-radio>
                </v-radio-group>
              </div>
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
    items: [
        {
            'text': 'Абаш',
            'value': 'atbash'
        },
        {
            'text': 'Цезаря',
            'value': 'caesar'
        }
    ],
    celectedCipher: '',
    radios: 'radio-1',
    input: '',
    output: '',
    key: '',
    checkbox: true,
  }),
  methods: {
    greet() {
      if (this.celectedCipher === this.items[0].value) {
        fetch(`atbash?text=${this.input}`)
          .then(function(response) {
              return response.json();
          })
          .then(json => {
              this.output = json.text;
          })
          .catch(err => console.error(err));
      } else if (this.celectedCipher === this.items[1].value) {
        fetch(`caesar?text=${this.input}&key=${this.key}&encrypt=${this.radios}`)
          .then(function(response) {
              return response.json();
          })
          .then(json => {
              this.output = json.text;
          })
          .catch(err => console.error(err));
      }
    },

    cleanInput() {
        this.input = '';
    },

    cleanOutput() {
        this.output = '';
    },

    reverse(){
        [this.input, this.output] = [this.output, this.input]
    }
  }
}
</script>
