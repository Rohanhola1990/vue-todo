<template>
    <div class="header">
        <div v-if="showinput" class="enterName" @keypress.13="activateButton">
            <input type="text" v-model="username" v-if="showinput" name="name" placeholder="Enter your name to begin...">
            <input type="button" value="Submit" v-if="username" @click="activateButton">
        </div>
        <div class="showHeader" v-show="nameState">
            <h2>
                {{ username }}'s To-do List
            </h2>
        </div>
    </div>
</template>


<script>

export default {
    data() {
        return{
            nameState: false,
            showinput: true,
            username: ''
        }
    },
    methods: {
        startList() {
            this.nameState = true
        },
        activateButton() {
            this.nameState = true
            this.showinput = false
        }
    }
}
</script>

<style scoped>
.enterName {
    height: 50px;
    display: flex;
    align-items: center;
}
.enterName input {
    height: 100%;
    border-radius: 3px;
    border: none;
    transition: all ease 0.4;
}
.enterName input[type=text] {
    flex: 1 1 80%;
    padding: 5px 15px;
}
.enterName input[type=text]:focus {
    box-shadow: 0 0 15px rgba(0,0,0,0.05);
}
.enterName input[type=button] {
    flex: 0 0 20%;
    cursor: pointer;
    margin-left: 12px;
    background-color: #333;
    color: #fff;
}
.showHeader {
    color: #333;
    text-align: center;
    text-transform: capitalize;
    padding: 15px 8px;
    background-color: aliceblue;
    box-shadow: 0 0 15px rgba(0,0,0,0.02);
    border-radius: 3px;
}
</style>

