<template>
    <div class="twoot-item" @click="favouriteTwoot(twoot.id)">
            <div class="twoot-item__twoot">
                <div class="twoot-item__user">
                    @{{ username }}
                    
                </div>
                <div class="twoot-item__content">
                    {{ twoot.content }}
                </div>
                <div class="twoot-item__added-on">Added: {{ hoursFromNow(todaysDate,twoot.date) }} ago</div>
            </div>  
    </div>
</template>


<script>
import moment from 'moment'
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
      created: function () {
        this.moment = moment;
    },
    setup(props){

        function favouriteTwoot(id){
            this.$emit('favourite', id);
        }
        function hoursFromNow(todaysDate, addedDate){
            let createdTime = moment.duration(todaysDate.diff(addedDate));
            const createdTimeInHours = Math.floor(createdTime.asHours());
            if (Math.floor(createdTime.asSeconds) <= 0){
                createdTime = "1 s";
            }
            else if (Math.floor(createdTime.asSeconds) < 60){
                createdTime = Math.floor(createdTime.asSeconds()) + " m";
            }
            else if(createdTimeInHours < 1 ){
                    createdTime = Math.floor(createdTime.asMinutes()) + " m";
            }
            else if(createdTimeInHours >= 1 && createdTimeInHours < 24){
                    createdTime = Math.floor(createdTime.asHours()) + " h";
            }
            else if(createdTimeInHours >= 1 && createdTimeInHours < 169){
                createdTime = Math.floor(createdTime.asDays()) + " days";
            }
            else if(createdTimeInHours > 169 && createdTimeInHours < 8800){
                createdTime = Math.floor(createdTime.asMonths()) + " months";
            }
            else if(createdTimeInHours > 8800){
                createdTime = Math.floor(createdTime.asYears()) + " years";
            }
            return createdTime
        }
        let todaysDate = moment(new Date());
        return{
            props,
            favouriteTwoot,
            todaysDate,
            hoursFromNow
        }
    }
    

};
</script>

<style lang="scss" scoped>
    .twoot-item{
        padding: 30px 50px;
        box-shadow: 0px 0px 10px 0px rgba(0, 0, 0, 0.6);
        border-radius: 5px;
        cursor: pointer;
        transition: all 0.3s ease;
        width: 100%;
        background-color: #2e2e2e;
        margin: 5px 0;
        color: #e1e1e1;
        &:hover{
        transform: scale(1.1, 1.1);

        }
        .twoot-item__content{
            padding: 10px 0 15px;
        }
        .twoot-item__user{
        margin-bottom: 5px;
        font-size: 0.9em;
        font-weight: 600;
        display: flex;
        justify-content: flex-start;
        align-items: baseline;
        }
        .twoot-item__added-on{
            font-size: 0.8em;
            opacity: .8;
            
        }
    }



</style>