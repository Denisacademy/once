<template>
  <div class="notes">
    <div class="note"  style="{color: level}" 
      :class="{full: !grid}" 
      v-for="(note, index) in notes" 
      :key="index">
      <div class="note-header" :class="{full: !grid}">
        <p>{{ note.title }}</p>
        <p 
          style="cursor: pointer;" 
          @click="removeNote(index)">x</p> 
      </div>
      <!-- index $emit -->
      <div class="note-body">
        <p>{{ note.descr }}</p>
        <span>{{ note.date }}</span>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    props: {
      notes: {
        type: Array,
        required: true
      },
      grid: {
        type: Boolean
      },
      level: {
        type: String,
        required: true
      }
    },
    methods: {
      removeNote(index) { 
        console.log(index);
        this.$emit('remove', index) //index as element
      }
    }
  }
</script>

<style>
body {
  background: #ddd;
}
  .notes {
    display: -webkit-flex;
    display: -moz-flex;
    display: -ms-flex;
    display: -o-flex;
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex-wrap: wrap;
    padding: 40px 0; 
  }

  .note {
    width: 44%;
    padding: 18px 20px;
    margin-bottom: 20px;
    background-color: white;
    transition: all .25s cubic-bezier(.02, .01, .47, 1);
/*    background: red;
*/  }

  .note:hover {
    box-shadow: 0 30px 30px rgba (0, 0, 0, .04);
    transform: translate(0, -6px);
    transitiont-delay: .5;
  }

  .full {
    width: 100%;
    text-align: center;
  }
  
  .note-header {
    display: -webkit-flex;
    display: -moz-flex;
    display: -ms-flex;
    display: -o-flex;
    display: flex;
    align-items: center;
    justify-content: space-between;
    p {
      color: #402caf;
      font-size: 22px;
    }
  }

  .note-header.full {
    text-align: center;
  }
  
  h1{
    font-size: 22px;
  }
  .note-body {
    p {
      margin: 20px 0;
    }
    span {
      font-size: 14px;
      color: 999;
    }
  }

  span {
    margin-right: 12px; 
    color: #999;
  }

  .active {
    color: orange;
  }

  span:last-child {
    margin-right: 0;
   
  }

</style>