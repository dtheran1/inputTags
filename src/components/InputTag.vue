<script>
import { ref } from 'vue';

export default {
  setup() {
    const currentValue = ref('')
    const tags = ref([])

    const handleSubmit = () => {
      if (!currentValue.value) return
      // console.log(currentValue.value);

      const exist = tags.value.some(item => item === currentValue.value)
      if (exist) return

      tags.value.push(currentValue.value)
      currentValue.value = ''
    }

    const handleKeyDown = (e) => {
      if (e.key === 'Backspace' && currentValue.value === '')
        tags.value.pop()
    }

    const deleteTag = (tag) => {
      tags.value = tags.value.filter(item => item !== tag)
    }

    return { currentValue, handleKeyDown, tags, deleteTag, handleSubmit }
  }
}


</script>
<template>
  <div class="inputTag">
    <div class="tags">
      <div class="tag" v-for="(tag, ind) in tags" :key="tag">
        {{ ind + 1 }}. {{ tag }} <button @click="deleteTag(tag)">x</button>
      </div>
    </div>
    <form @submit.prevent="handleSubmit">
      <input class="input" type="text" v-model="currentValue" @keydown="handleKeyDown">
    </form>
  </div>
</template>
<style scoped>
.inputTag {
  display: inline-flex;
  border: solid 1px #5e7410;
  border-radius: 5px;
  height: 43px;
}

.tags {
  display: flex;
  gap: 3px;
  padding: 5px;
}

.tags .tag{
  display: flex;
  padding: 5px;
  border: solid 1px #1e7969;
  gap: 5px;
  align-items: center;
  border-radius: 3px;
}

.inputTag form{
  display: inline-flex;
}

.inputTag .input {
  border: none;
  outline: none;
  padding: 0 5px;
  background: #3b504c;
  color: antiquewhite;
}

.tag button {
  background-color: transparent;
  border: none;
  border-radius: 3px;
  font-size: 15px;
  cursor: pointer;
  color: red;
}

.tag button:hover {
  background: #704e4e;
}
</style>