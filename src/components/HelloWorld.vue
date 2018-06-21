<template>
  <div class="hello">
    <h1>{{ msg }}</h1>

  <form @submit.prevent="getFormValues">

    <!--Text field-->
    <div class="div-margin">
      <b>Input</b>
      <input type="text" id="input" v-model="input_val"> <span v-text="input_val"></span>
    </div>

    <div class="div-margin">
      <b>Textarea:</b>
      <textarea v-model="message" id="textarea"></textarea>
      <span>{{ message }}</span>
    </div>
     <!--Checkbox-->
    <div id='example-3' class="div-margin">
      <b>Checkbox</b>
      <input type="checkbox" id="checkbox1" value="Jack" v-model="checkedNames">
      <label for="checkbox1">checkbox1</label>
      <input type="checkbox" id="checkbox2" value="John" v-model="checkedNames">
      <label for="checkbox2">checkbox2</label>
      <input type="checkbox" id="checkbox1" value="Mike" v-model="checkedNames">
      <label for="checkbox3">checkbox3</label>
      <br>
      <span>Checked names: {{ checkedNames }}</span>
    </div>

    <!--Radio button-->
    <div class="div-margin">
      <b>Radiobox</b><br>
      <input type="radio" id="radio1" value="One" v-model="picked">
      <label for="radio1">radio1</label>
      <br>
      <input type="radio" id="radio2" value="Two" v-model="picked">
      <label for="radio2">radio2</label>
      <br>
      <span>Picked: {{ picked }}</span>
    </div>

    <!--Select box-->
    <div class="div-margin">
       <b>Selectbox</b><br>
      <select v-model="selected">
        <option disabled value="">Please select one</option>
        <option>A</option>
        <option>B</option>
        <option>C</option>
      </select>
      <span>Selected: {{ selected }}</span>
    </div>

    <!--Image-->
    <div class="div-margin">
       <b>ImageUpload</b><br>
        <input type="file" id="imagefile" />
    </div>

    <div class="div-margin">
      <button class="btn btn-primary">You've clicked this button {{counter}} times!</button>
    </div>

  </form>

  </div>
</template>



<script>
export default {
  name: "hello",
  data() {
    return {
      msg: "Welcome to Your Vue.js App",
      input_val: "",
      message: "",
      checkedNames: [],
      picked: "",
      selected: "",
      imaging: "",
      counter: 1,
      output: ''
    };
  },
  methods: {
    getFormValues (submitEvent) {
      this.input = this.input_val;
      this.textarea = this.message;
      this.checkbox = this.checkedNames;
      this.radio = this.picked;
      this.selectbox = this.selected;
      this.image = submitEvent.target.elements.imagefile.value;
     // this.getData();
      this.postData();
    },
    // get data from an url or api
    getData: function () {
      let self = this
      const myRequest = new Request('https://jsonplaceholder.typicode.com/posts')
      fetch(myRequest)
        .then((response) => {
              return response.json()
            })
        .then((data) => {
          self.items = data
          console.log(self.items)
        }).catch( error => { console.log(error); });
    },
    // post data from an url or api
    postData: function(){
      let self = this
      const url = new Request('http://127.0.0.1:9000/')
      fetch(url, {
          method: 'post',
          // headers: {
          //   "Content-type": "application/x-www-form-urlencoded; charset=UTF-8"
          // },
          // body: 'foo=bar&lorem=ipsum'
          headers: {
            "Content-type": "application/json"
          },
          body: JSON.stringify({
            name: this.input,
            login: 'hp',
          })
        })
        .then(json)
        .then(function (data) {
          console.log('Request succeeded with JSON response', data);
        })
        .catch(function (error) {
          console.log('Request failed', error);
        });
    }
  }

};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-position: inside;
}
a {
  color: #42b983;
}

.div-margin {
  margin-top: 2rem;
  margin-bottom: 2rem;
}
</style>
