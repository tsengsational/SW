<template>
    <div class="hello">
        <h1>List of characters</h1>
        <button v-on:click="sendData()">Send</button>
        <br />
        <br />
         <li>{{input.name[0]}} -- {{input.name[1]}} -- {{input.name[2]}} -- {{input.name[3]}} -- {{input.name[4]}} -- {{input.name[5]}} -- {{input.name[6]}} -- {{input.name[7]}} -- {{input.name[8]}}</li>
         <br />
         <br />
         <input id="txtName" @keyup.enter="getData('txtName')" v-model="txtInput" type="text">
    </div>

</template>

<script>
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
            sendData() {
                this.$http.get("https://swapi.co/api/people/?format=json", { headers: { "content-type": "application/json" } }).then(result => {
                this.input.name[0] = result.data.results[0]["name"]; this.input.name[1] = result.data.results[1]["name"]; this.input.name[2] = result.data.results[2]["name"]; this.input.name[3] = result.data.results[3]["name"]; this.input.name[4] = result.data.results[4]["name"]; this.input.name[4] = result.data.results[4]["name"]; this.input.name[5] = result.data.results[5]["name"]; this.input.name[6] = result.data.results[6]["name"]; this.input.name[7] = result.data.results[7]["name"]; this.input.name[8] = result.data.results[8]["name"];
                }, error => {
                    console.error(error);
                });
            },
            getData(txtName) {return console.log(this.input.name.includes(this.txtInput))}
    }
    }
</script>

<style scoped>
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
