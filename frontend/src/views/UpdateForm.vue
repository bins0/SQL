<template>
    <div>
        <input type="text" v-model="memo.title"><br>
        <textarea cols="30" rows="10" v-model="memo.memo"></textarea><br>
        <button @click="updateform">수정</button>
    </div>
</template>

<script>
export default {
    data(){
        return {
            memo :{
                title:'',
                memo:''
            }
        }
    },
    created (){
        this.$http.get(`/api/memo/${this.$route.params.id}`)
        .then((response)=>{
            this.memo = response.data
        })
    },
    methods : {
        updateform(){
            this.$http.put('/api/memo/updateform',{
                data :{
                    memo:this.memo
                }
            }).then((response) => {
                console.log(response.data)
            })
            this.$router.push('/')
        }
    }
}
</script>