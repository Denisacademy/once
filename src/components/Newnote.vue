<template>
  <div class="new-note" >
    <label>Title</label>
    <input v-model="note.title" type="text">
    <label >Description</label>
    <textarea v-model="note.descr"></textarea>
    <button class="btn btnPrimary" @click="addNote">New note</button>
    <!-- Собираем данные и перекидываем родителю -->
  </div>
</template>


<script>
  export default {
    data() {
      return {
        
      }
    },
    props : {
      note: {
        type: Object,
        required: true
      },
      level: {
        type: String,
        required: true
      }
    },
    methods: {
      addNote() {
        this.$emit('takeThat', this.note, this.level)
      }
    }
  }
</script> 

<style>
  .new-note {
    text-align: center;
  }
.extreme {
  background: red;

}
.default {
  background: white;
  
}
.important {
  background: orange;
  
}

</style>