
<template>
  <div>
    <h1>Create</h1>
    <form v-on:submit.prevent="addItem">
      <div class="row">
        <div class="col-md-6">
          <div class="form-group">
            <label>Item Name:</label>
            <input type="text" class="form-control" v-model="item.name">
          </div>
        </div>
        </div>

        <div class="row">
                  <div class="col-md-6">
                    <div class="form-group">
                      <label>Raw text:</label>
                      <textarea class="form-control col-md-6" v-model="item.text" rows="40" style="resize: none"></textarea>
                    </div>
                  </div>
                  <div class="col-md-6">
                    <div class="form-group">
                      <label>Markdown text:</label>
                      <div v-html="compiledMarkdown"></div>
                    </div>
                  </div>
        </div>
        <br />
        <div class="form-group">
          <button class="btn btn-primary">Add Item</button>
        </div>
    </form>
  </div>

</template>
<script>
    const marked = require("marked");
    const config = require('../../config/DB');
    export default {
        data(){
            return{
                item:{text: '# Hello'}
            }
        },
        computed: {
            compiledMarkdown: function () {
                return marked(this.item.text, { sanitize: true })
            }
        },
        methods: {
            addItem(){
                let uri = 'http://localhost:4000/items/add';
                this.axios.post(uri, this.item).then((response) => {
                    this.$router.push({name: 'DisplayItem'})
                })
            }
        }
}
</script>
