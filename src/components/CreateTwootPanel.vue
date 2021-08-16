<template>
        <form class="user-card__new-twoot" @submit.prevent="createNewTwoot">
                    <label for="new_twoot">Add new twoot</label>
                    <textarea name="new_twoot" id="new_twoot" rows="4" width="80" v-model="newTwootContent" :class="{'--exceeded': newTwootCharacterCount >= 80}"></textarea>
                    <span>{{newTwootCharacterCount}}/80</span>
                <div class="user-card__create-twoot-type">
                    <label for="twoot_type">Type: </label>
                        <select name="twoot_type" id="twoot_type" v-model="selectedTwootType">
                            <option :value="option.value" v-for="(option,index) in twootTypes" :key="index" >
                            {{ option.name }}
                            </option>   
                        </select>
                </div>
                <button class="user-card__submit-twoot">Submit twoot</button>
      </form>
</template>

<script>
export default {
    name: "CreateTwootPanel",
    data(){
        return{
        newTwootContent: '',
        selectedTwootType: 'instant',
        twootTypes: [
          {value: 'draft', name: 'Draft'},
          {value: 'instant', name: 'Instant twoot'}
        ]
        }
    },

    computed: {
            newTwootCharacterCount(){
      return this.newTwootContent.length;
            }
    },
    methods: {
    createNewTwoot(){
      if(this.newTwootContent && this.selectedTwootType !== 'draft'){
        this.$emit('add-twoot',this.newTwootContent)
        this.newTwootContent = '';
      }
      
    }
    }
};
</script>