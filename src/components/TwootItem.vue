<template>
    <div class="twoot-item" @click="favouriteTwoot(twoot.id)">
            <div class="twoot-item__twoot">
                <div class="twoot-item__user">
                    @{{ username }}
                </div>
                <div class="twoot-item__content">
                    {{ twoot.content }}
                </div>
            </div>  
    </div>
</template>


<script>
export default {
    name: "TwootItem",
    props: {
        username: {
            type: String,
            required: true
        },
        twoot: {
            type: Object,
            requred: true
        }
    },
    methods: {
        favouriteTwoot(id){
            this.$emit('favourite', id);
        }
    }
};
</script>

<style lang="scss" scoped>
    .twoot-item{
        padding: 30px 50px;
        box-shadow: 0px 0px 10px 0px rgba(255,255,255,0.6);
        border-radius: 5px;
        cursor: pointer;
        transition: all 0.3s ease;
        width: 100%;
        background-color: white;
        border: 1px solid transparent;
        margin: 5px 0;
        &:hover{
        transform: scale(1.05, 1.05);
        border-color: darkgray;
        }
        .twoot-item__user{
        margin-bottom: 5px;
        font-size: 0.9em;
        font-weight: 600;
        }
    }



</style>