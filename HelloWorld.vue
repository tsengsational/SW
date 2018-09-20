<template>
    <div class="hello">
        <h1>List of characters</h1>
        <button v-on:click="sendData()">Send</button>
        <br />
        <br />
        <!-- this is hardcoded. try using the v-for directive to do this dynamically -->
        <!-- you're also going to want to break these up into different `li`, no? Especially if they need their own event listeners. -->
         <li>{{input.name[0]}} -- {{input.name[1]}} -- {{input.name[2]}} -- {{input.name[3]}} -- {{input.name[4]}} -- {{input.name[5]}} -- {{input.name[6]}} -- {{input.name[7]}} -- {{input.name[8]}}</li>
         <br />
         <br />
         <!-- no need to get data on keyup when you are using v-model. The input value is bound to a property on your data object, unless the `getData()` function has another use that I'm not seeing. -->
         <input id="txtName" @keyup.enter="getData('txtName')" v-model="txtInput" type="text">
    </div>

</template>

<script>
// how are you loading the initial characters into the component?

    export default {
        data () {
            return {
                txtInput: "",
                list: "",
                input: {
                    results: "",
                    name: [],
                    films: ""
                }
            }
        },
        methods: {
            // prioritize readability over conservation of lines. If no one can understand what you're coding it's useless when working on a team.
            // why did you choose to use VueResource and the $http library? Wouldn't it be easier to just use the native fetch api?
            // Error handling should be handled in a `.catch()`
            sendData() {
                this.$http.get("https://swapi.co/api/people/?format=json", { headers: { "content-type": "application/json" } }).then(result => {
                this.input.name[0] = result.data.results[0]["name"]; this.input.name[1] = result.data.results[1]["name"]; this.input.name[2] = result.data.results[2]["name"]; this.input.name[3] = result.data.results[3]["name"]; this.input.name[4] = result.data.results[4]["name"]; this.input.name[4] = result.data.results[4]["name"]; this.input.name[5] = result.data.results[5]["name"]; this.input.name[6] = result.data.results[6]["name"]; this.input.name[7] = result.data.results[7]["name"]; this.input.name[8] = result.data.results[8]["name"];
                }, error => {
                    console.error(error);
                });
            },
            // single line functions like this aren't very readable. Better to break this up over a few lines like the above function
            getData(txtName) {return console.log(this.input.name.includes(this.txtInput))}
    }
    }
</script>

<style scoped>
// try and style with class selectors, simply using top-line selectors is not adaptable and can create inadvertant styling rule collisions. The more specific you can be with your selectors, the better.;

    h1, h2 {
        font-weight: normal;
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

    textarea {
        width: 600px;
        height: 200px;
    }
</style>
