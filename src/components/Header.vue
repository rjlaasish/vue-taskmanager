<template>
    <header>
        <h1>{{ title }}</h1>
      <Button :text="showAddTask?'Close':'Add Task'" @add-task-btn="$emit('add-task-btn')" :color="!showAddTask?'green':'red'"/>
    </header>
</template>


<script>
import Button from './Button';
export default {
    name:'Header',
  props:['title','showAddTask'],
  components:{
      Button
  },
  methods:{
      handleClick(){

      }
  }
}
</script>

<style scoped>
header{
display:flex;
justify-content: space-between;
align-items:center;
margin-bottom:20px;

}

</style>