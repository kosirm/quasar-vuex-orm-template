<template>
  <q-page class="q-pa-xl">
    <h1>{{user.name}}</h1>
    <input type="text" v-model="form.title">
    <button @click="addList">Add List</button>
    <List v-for="list in user.lists" :key="list.id" :list="list"></List>
  </q-page>
</template>

<script>
import User from '../store/classes/User'
import ListComponent from '../components/List'
import List from '../store/classes/List'
export default {
  name: 'PageIndex',
  components: {
    List: ListComponent
  },
  data() {
    return {
      form: {
        title: '',
        user_id: 28
      }
    }
  },
  computed: {
    user() {
      return User.query()
        .with('lists')
        .find(28)
    }
  },
  methods: {
    addList() {
      // console.log(this.form)
      List.insert({ data: this.form })
    }
  },
  beforeMount() {
    User.insert({
      data: [
        {
          id: 28,
          name: 'Milan',
          email: 'testuser2@example.com'
        },
        {
          id: 27,
          name: 'Lidija',
          email: 'testuser1@example.com'
        }
      ]
    })
  }
}
</script>
