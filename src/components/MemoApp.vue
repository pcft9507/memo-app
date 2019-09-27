<!-- src/components/MemoApp.vue -->
<template>
  <div class="memo-app">
    <memo-form @addMemo="addMemo"/>
    <ul class="memo-list">
      <memo/>
    </ul>
  </div>
</template>

<script>
import MemoForm from './MemoForm';
import Memo from './Memo';

export default {
  name: 'MemoApp',
  components: {
    MemoForm,
    Memo
  },
  data () {
    return {
      memos: []
    }
  },
  created () {
    this.memos = localStorage.memos ? JSON.parse(localStorage.memos) : [];
  },
  methods: {
    addMemo (played) {
      // MemoForm에서 올려 받은 데이터를 먼저 컴포넌트 내부 데이터에 추가한다.
      this.memos.push(played);
      // 내부 데이터를 문자열로 변환 후, 로컬 스토리지에 저장한다.
      this.storeMemo();
    },
    storeMemo () {
      const memosToString = JSON.stringify(this.memos);
      localStorage.setItem('memos', memosToString);
    }
  },
}
</script>

<style scoped>
  .memo-list {
    padding: 20px 0;
    margin: 0;
  }
</style>