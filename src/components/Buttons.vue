<div>
  <template>
    <el-row>
      <el-button type="primary" @click = sendQuery>Press me</el-button>
      <el-button type="primary">Press me</el-button>
      <el-button type="primary">Press me</el-button>
      <el-button type="primary">Press me</el-button>
      <el-button type="primary">Press me</el-button>
      <el-button type="primary">Press me</el-button>
      <el-button type="primary">Press me</el-button>
      <el-button type="primary">Press me</el-button>

    </el-row>
  </template>

  <template>

    <el-table
              :data="data"
              style="width: 100%">
      <el-table-column
              prop="date"
              label="Date"
              width="180">
      </el-table-column>
      <el-table-column
              prop="name"
              label="Name"
              width="180">
      </el-table-column>
      <el-table-column
              prop="address"
              label="Address">
      </el-table-column>
    </el-table>

  </template>

</div>

<script>
  import axios from 'axios'
export default {
  name: 'HelloWorld',
  props: {
    msg: String,
    data: []
  },
  methods:{
    sendQuery(){

      var query = "PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> \
              PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>\
              SELECT * WHERE {?sub ?pred ?obj .}LIMIT 10"
      //var param = {"query":query}
      const headers = {'Content-Type': 'application/x-www-form-urlencoded; charset=utf-8'}
      const endpoint = 'http://3d3c8850.ngrok.io/project'
      axios.post(
              endpoint,
              encodeURI('query='+query+'&format=json'),
              {headers:headers})
              .then((function (response) {
        // eslint-disable-next-line no-console
                  console.log(response)
                  this.data = response.data.results.bindings
              })
      )
    }
  }
}
</script>
