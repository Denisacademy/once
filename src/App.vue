<template>
  <div class="wrapper">
    <div class="wrapper-content">
      <section>
        <div class="container">
          <select   v-model="level">
            <option selected value="white">default</option>
            <option value="orange">important</option>
            <option value="red">extreme</option>
          </select>

          <select @change = 'showLevel()' v-model="filter">
            <option selected value="white">Стандарт</option>
            <option value="orange">Важные</option>
            <option value="red">Критические</option>
          </select>


<!--              <h1> {{ title }} </h1>
 -->
          <!-- скрываем блок, чтобы не было ошибки -->
            
            <message :message="message" v-if="message"/>
            <!-- new note -->
            <newnote 
           

            
              :level="level" 
              @takeThat="addNote" 
              :note="note"/>
<!--             <div class="new-note">
              <input v-model="note.title" type="text">
              <textarea v-model="note.descr"></textarea>
              <button @click="addNote">New note</button>
            </div> -->
            <div class="note-header">
              <h1> {{ title }} </h1>
              <!-- Search**** -->
              <!--**children waits for search from parent but props is 'value'  **-->
             <search 
                @search="search = $event" 
                :value="search" 
                placeholder="Find your note"/>
                <!--**** icons control ***-->

              <div class="icons">
                <span 
                  style="cursor: pointer" 
                  @click="grid=false" 
                  :class="{active: grid}">&#247;  </span>
                <span 
                  style="cursor: pointer" 
                  @click="grid=true" 
                  :class="{active: !grid}">&Xi;   </span>
              </div>
            </div>
          <!-- note list -->

<!--           <div class="notes">
            <div class="note" v-for="(note, index) in notes" :key="index">
              <div class="note-header">
                <p>{{ note.title }}</p>
              </div>
              <div class="note-body">
                <p>{{ note.descr }}</p>
                <span>{{ note.date }}</span>
              </div>
            </div>
          </div> -->

<!--         <notes :grid="grid" @remove="removeNote" :notes="notes"/>
 -->        <notes 

               :level="level" 
               :grid="grid" 
               @remove="removeNote" 
               :notes="notesFilter"/>
        
        </div>
      </section>
      <h1 @click="showLevel">Render</h1>
    <div v-for="note in showLevel" :key="note.title">
      <p>{{note}}</p>
    
    </div> 



        </div>  
  </div>
</template>

<script>
import message from '@/components/Message.vue'
import newnote from '@/components/Newnote.vue'
import notes from '@/components/Notes.vue'
import search from '@/components/Search.vue'

export default {
  components: {
    message,
    newnote,
    notes,
    search
  },
  data() {
    return {
      title: 'Notes App',
      search: '',
      message: null,
      grid: true,
      level: 'white',
      filter: '',
      colors: {
          default: 'white',
          important: 'orange',
          extreme: 'red'
        },
      note: {
        title: '',
        descr: '',
        level: 'white'     
      },
      notes: [
        {
          title: 'First Note',
          descr: 'Description for first note',
          date: new Date(Date.now()).toLocaleString(),
          level: 'white'
        },
        {
          title: 'Second Note',
          descr: 'Description for second note',
          date: new Date(Date.now()).toLocaleString(),
          level: 'white'
        },
        {
          title: 'Third Note',
          descr: 'Description for third note',
          date: new Date(Date.now()).toLocaleString(),
          level: 'white'
        }
      ]
    }
  },
  methods: {
    setColor() {
      setTimeout(() => {
        document.querySelector('.notes').lastChild.style.background = this.level 
        this.level = 'white'
  }, 10);

    },

    addNote () {
      let {title, descr, level} = this.note
      console.log(level);
      if (title === '') {
        this.message = 'title can`t be blank!'
        return false
      }

      this.notes.push({
        title,
        descr,
        date: new Date(Date.now()).toLocaleString(),
        level: this.level
      })
      this.message = null
      this.note.title = ''
      this.note.descr = ''


      let add = document.querySelectorAll('.note')
      this.setColor()
   
    },
    removeNote(index) {
      this.notes.splice(index, 1)
    },
    showLevel() {
      return [1,3,5,7,9]
      // console.log(this.filter)
      let filter = this.notes
      filter = filter.filter(el => {
        if(el.level === this.filter) return el
        // console.log(el.level)
      })
      console.log(filter);
      return filter  
          
    }
  },
  computed: { //ready to change notes
    notesFilter() {
      // this.showLevel();
      let array = this.notes,
          search = this.search
          
      if(!search) {
      // console.log(array, search); 
      return array //if  search not true - '' , return all nassive 
     }  // Small
      search = search.trim().toLowerCase()   //remove gaps
        //Filter
      array = array.filter(note => {
        if(note.title.toLowerCase().indexOf(search) > -1 ) return note // !== -1
        })
        return array
    }
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

.icons span {
  font-size: 46px;
}
</style>
