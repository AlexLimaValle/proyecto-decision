<template>
    <div class="all bg-dark">
        <img v-if="imagen" :src="imagen" class="imagen" alt="imagen">
        <div class="container" id="form">
            <div class="row justify-content-center">
                <div class="col-5 mt-5">
                    <input class="form-control" type="text" v-model="question">
                    <p v-if="response" class="lead fs-1 mt-5 text-center text-light">{{response}}</p>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data(){
        return{
            question:null,
            response:null,
            imagen:null,
        }
    },methods:{
        
        async getResponse(){
            this.response = "pensando...."
            const api = await fetch("https://yesno.wtf/api");
            const {answer,image} = await api.json();
            this.response = (answer == "yes")?"SI":"NO";
            this.imagen = image;
        }

    },watch:{
        question(newmessage){
            if(!newmessage.includes("?")) return;
            this.getResponse();
        }
    }
}

</script>

<style>
    .all{
        width:100%;
        height:100%;
        position: relative;
    }

    .imagen{
        width:100%;
        height:100%;
        position:absolute;
        z-index: 1;
    }

    #form{
        position: relative;
        z-index:10;
    }
</style>