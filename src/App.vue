<template>
  <div class="container p-5" >
    <div class="row">
      <div class="col-9">
        <div id="red-red"
            @drop="onDrop($event)" @dragover.prevent class="card mb-4"
             style="background: grey;
             height: 100%;
             background-size: cover;
             background-repeat: no-repeat;">

          <!--New List-->
            <Draggable bounds="#red-red"
                       v-for="user in stageList"
                       :key="user.user">
          <img  class="stage-list-div"
              :src="user.picture"

                style="  resize: both;width: 124px; height: 124px; background-size: contain;">

            </Draggable>

          <!--New List-->

        </div>
      </div>



      <div class="col-3">
        <div v-for="user in myUsers" :key="user.user">
          <div class="my-card card bg-light mb-3" >
            <div class="card-header" dir="rtl">  {{user.user}} | {{user.name}}</div>
            <div class="card-body">
              <div class='drag-el' draggable="true" @dragstart="startDrag($event, user)"
                   :style="{backgroundImage: 'url('+user.picture+')'}"
                   style="width: 124px; height: 124px; background-size: contain;"></div>
            </div>

          </div>
        </div>
      </div>

    </div>

    <div>

    </div>


    <div class="float-start">
      <button type="btn" @click="PrintDiv"
              class="btn btn-primary mt-3 mb-5">
        Download Image
      </button>
    </div>

  </div>



  <div class="clear-fix"></div>

</template>

<script>
import axios from "axios";
import html2canvas from "html2canvas";

export default {
  name: 'App',
  data() {
    return {
      myUsers: '',
      stageList: []
    }
  },
  computed: {
    listOne () {
      return this.myUsers.filter(item => item.user === 1)
    },
  },
  methods: {
    startDrag (evt, item) {
      evt.dataTransfer.dropEffect = 'move'
      evt.dataTransfer.effectAllowed = 'move'
      evt.dataTransfer.setData('itemID', item.user)
    },
    PrintDiv() {
      var theelement = document.getElementById('red-red');
      html2canvas(theelement, {allowTaint: true,
        useCORS: true
      }).then(function(canvas) {
        canvas.toBlob(function(blob) {
          window.saveAs(blob, 'my_image.jpg');
        });
      });
},


    onDrop (evt) {
      const itemID = evt.dataTransfer.getData('itemID');
      this.myUsers.find(user => {
        // if() {
         return user.user == itemID ? this.stageList.push(user) : '';
        // } else {
        //
        // }
    })
    },

  },

  mounted() {
    axios.get('http://www.mocky.io/v2/59bd9a773c00001303529fe0').then(res => {
      return this.myUsers = res.data.users;
    }).catch( err =>{
      console.log(err)
    })
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.clear-fix {
  width: 100%;
  height: 200px;
}

.resizable-content {
  height: 200px;
  width: 200px;
  background-color: aqua;
}



</style>
