<template>
  <div class="memo-app">
    <memo-form @addMemo="addMemo"/>
    <ul class="memo-list">
      <memo v-for="memo in memos"
            :key="memo.id"
            :memo="memo"
            @deleteMemo="deleteMemo" 
            @updateMemo="updateMemo"
            :editingId="editingId"
            @setEditingId="SET_EDITING_ID"
            @resetEditingId="RESET_EDITING_ID"/>
    </ul>
  </div>
</template>
<script>
// import axios from 'axios';
import MemoForm from './MemoForm';
import Memo from './Memo';
import { mapState, mapActions, mapMutations } from 'vuex';
import { RESET_EDITING_ID, SET_EDITING_ID } from '../store/mutations-types';
// const memoAPICore = axios.create({
//   baseURL: 'http://localhost:8000/api/memos'
// })

export default {
  name: 'MemoApp',
  computed: {
    ...mapState([
      'memos',
      'editingId'
    ])
  },
  // data () {
  //     return {
  //         memos: [],
  //     }
  // },
  created() {
//      this.memos = localStorage.memos ? JSON.parse(localStorage.memos) : [];

    // memoAPICore.get('/')
    // .then(res => {
    //   this.memos = res.data;
    // })
    this.fetchMemos();
  },
  methods: {
    ...mapMutations([
      SET_EDITING_ID,
      RESET_EDITING_ID
    ]),
      ...mapActions([
        'fetchMemos',
        'addMemo',
        'deleteMemo',
        'updateMemo'
      ]),
  },
  components: {
    MemoForm,
    Memo
  }
};
</script>

<style scoped>
  .memo-list {
    padding: 20px 0;
    margin: 0;
  }
</style>
