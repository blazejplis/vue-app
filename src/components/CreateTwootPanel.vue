<template>
        <form class="user-card__new-twoot" @submit.prevent="createNewTwoot(state.newTwootContent)">
                    <label for="new_twoot">Add new twoot</label>
                    <textarea name="new_twoot" id="new_twoot" rows="4" width="80" v-model="state.newTwootContent" :class="{'--exceeded': newTwootCharacterCount >= 80}"></textarea>
                    <span>{{newTwootCharacterCount}}/80</span>
                <div class="user-card__create-twoot-type">
                    <label for="twoot_type">Type: </label>
                        <select name="twoot_type" id="twoot_type" v-model="state.selectedTwootType">
                            <option :value="option.value" v-for="(option,index) in state.twootTypes" :key="index" >
                            {{ option.name }}
                            </option>   
                        </select>
                </div>
                <button class="user-card__submit-twoot">Submit twoot</button>
      </form>
</template>

<script>
import { reactive,computed } from 'vue';
export default {
  name: "CreateTwootPanel",
  setup(props,ctx) {
    const state = reactive({
      newTwootContent: '',
      selectedTwootType: 'instant',
      twootTypes: [{
          value: 'draft',
          name: 'Draft'
        },
        {
          value: 'instant',
          name: 'Instant twoot'
        }
      ]
    })

    const newTwootCharacterCount = computed(() => state.newTwootContent.length)

    function createNewTwoot() {
      if (state.newTwootContent && state.selectedTwootType !== 'draft') {
        ctx.emit('add-twoot', state.newTwootContent)
        state.newTwootContent = '';
      }
    }

    return {
      state,
      newTwootCharacterCount,
      createNewTwoot
    }
  }
};
</script>