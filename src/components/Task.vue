<template>
    <div class="task">
        <div class="checkboxdiv">
            <input type="checkbox" class="largeCheckbox" v-model="isFinished" v-on:click="this.$parent.changeStateTask(index)">
        </div> 
        <div class="label" :class="{finished: isFinished}">    
            <p>{{task}}</p>
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
    margin-top: 8px;
    box-shadow: 5px 5px 10px 1px rgb(224, 224, 224, 0.5);
    border-radius: 5px;
}
.checkboxDiv{
    width: 70px;
}
.label{
    width: 100%;
    overflow: hidden;
    text-align: justify;
}
.label > p {
    font-size: 22px;
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
    width: 70px;
    position: relative;
    font-size: 20px;
    font-weight: 800;
    color: rgb(205, 92, 92);

}
.removeBtn>span{
    display: none;
    position: absolute;
    top: 30%;
}
.task:hover > .removeBtn > span{
    display: block;
}
</style>
