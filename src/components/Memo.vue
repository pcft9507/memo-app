<template>
  <li class="memo-item">
    <strong>{{ memo.title }}</strong>
    <p @dblclick="handleDblClick">
      <!-- 문단이 보이는 영역과 인풋 영역에 v-if와 v-else를 이용하여 조건문을 추가해준다. -->
      <!-- template 태그를 이용하여 제목 텍스트를 감싸준다. -->
      <template v-if="!isEditing">{{ memo.content }}</template>
      <input v-else
             type="text"
             ref="content"
             :value="memo.content"
             @blur="handleBlur"
             @keydown.enter="updateMemo"/>
    </p>
    <button type="button" @click="deleteMemo">
      <i class="fas fa-times"></i>
    </button>
  </li>
</template>

<script>
export default {
  name: 'Memo',
  props: {
    memo: {
      type: Object
    }
  },
  beforeUpdate () {
    console.log("beforeUpdate =>", this.$refs.content);
  },
  update () {
    console.log("update =>", this.$refs.content);
  },
  methods: {
    deleteMemo () {
      // 부모로부터 props로 내려받은 memo의 id를 부모 컴포넌트의 자용자 정의 이벤트인 deleteMemo 함수의 파라미터로 전달해준다.
      const id = this.memo.id;
      this.$emit('deleteMemo', id);
    },
    handleDblClick () {
      // 더블 클릭을 했을 때, 클릭한 메모의 수정 상태를 true로 변경한다.
      this.isEditing = true;
      console.log("handleDblClick =>", this.$refs.content);
      // content에 focus 이벤트를 추가한다.
      this.$nextTick(() => {
        this.$refs.content.focus();
      });
    },
    updateMemo (e) {
      const id = this.memo.id;
      const content = e.target.value.trim();
      if (content.length <= 0) {
        return false;
      }
      this.$emit('updateMemo', { id, content });
      this.isEding = false;
    },
    handleBlur () {
      this.isEditing = false;
    }
  },
  data () {
    return {
      isEditing: false
    }
  }
}
</script>

<style scoped>
  .memo-item {
    overflow: hidden;
    position: relative;
    margin-bottom: 20px;
    padding: 24px;
    box-shadow: 0 4px 10px -4px rgba(0, 0, 0, .2);
    background-color: #fff;
    list-style: none;
  }
  .memo-item button {
    background: none;
    position: absolute;
    right: 20px;
    top: 20px;
    font-size: 20px;
    color: #e5e5e5;
    border: 0;
  }
  .memo-item strong {
    display: block;
    margin-bottom: 12px;
    font-size: 18px;
    font-weight: normal;
    word-break: break-all;
  }
  .memo-item p {
    margin: 0;
    font-size: 14px;
    line-height: 22px;
    color: #666;
  }
  .memo-item p input[type="text"] {
    box-sizing: border-box;
    width: 100%;
    font-size: inherit;
    border: 1px solid #999
  }
</style>