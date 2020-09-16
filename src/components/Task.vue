<template>
    <div class="task">
        <div class="label" :class="{finished: isFinished}">
            <input type="checkbox" class="largeCheckbox" v-model="isFinished">
            <h2>{{task}}</h2>
        </div>
        <div class="removeBtn" v-on:click="removeTask(index)">
            <span>X</span>
        </div>
    </div>
    
</template>

<script>
export default {
    props: {
            index: {
                type: Number,
                required: true
            },
            task: {
                type: String,
                required: true
            },
            finished: {
                type: Boolean,
                required: true
            }
        },
    data() {
        return {
            isFinished: this.finished
        }
    },
    methods: {
        removeTask(index){
            this.$parent.removeTask(index);
        } 
    }
}
</script>

<style scoped>
.task{
    display: flex;
}
.label{
    display: flex;
    width: 90%;
}
.finished{
    color: rgb(110, 110, 110);
    text-decoration: line-through;
}
input.largeCheckbox{
    width: 30px;
    height: 30px;
    margin: 20px;
}
.removeBtn{
    display: none;
    width: 10%;
    position: relative;
    font-size: 20px;
    font-weight: 800;
    color: rgb(205, 92, 92);

}
.task:hover > .removeBtn{
    display: block;
}
.removeBtn>span{
    position: absolute;
    top: 30%;
}
</style>
