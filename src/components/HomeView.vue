<template>
  <div>
    <!-- Section 1: Text Interpolation -->
    <h2>Template Syntax</h2>
    <button @click="increment">Count</button>
    <button @click="decrement">Decrement count</button>
    <div>{{ count }}</div>
    <div>{{ arrayOfEmoji }}</div>

    <!-- Section 2: Class and Style Bindings -->
    <h2>Class and Style Bindings</h2>
    <div :class="{ active: isActive, 'text-success': count >= 5 }">Class</div>
    <div :style="{ color: textColor, fontSize: fontSize + 'px' }">Style</div>

    <!-- Section 3: Event Handling -->
    <h2>Event Handling</h2>
    <button @click="toggleEmoji">Toggle Emoji</button>
    <div v-if="showEmoji">{{ arrayOfEmoji }}</div>

    <!-- Section 4: Form Input Bindings -->
    <h2>Form Input Bindings</h2>
    <input type="text" v-model="inputText" />
    <input type="checkbox" v-model="inputCheckbox" />
    <input type="radio" v-model="radioValue" value="option1" />
    <select v-model="selectedFruit">
      <option value="Die">Die</option>
      <option value="Live">Live</option>
    </select>
    <textarea v-model="textareaText"></textarea>

    <!-- Section 6: List Rendering -->
    <h2>List Rendering</h2>
    <ul>
      <li v-for="(item, index) in items" :key="index">{{ item.name }}</li>
    </ul>

    <!-- Section 7: Event Handling -->
    <h2>Event Handling</h2>
    <button class="button" @click="inlineClickHandler">Inline Click</button>

   
  </div>
</template>

<script>
import { ref, computed, watch } from 'vue';

export default {
  props: {
    emoji: { type: String, default: '👽' }
  },
  setup(props) {
    // Data properties
    const count = ref(0);
    const inputText = ref('');
    const inputCheckbox = ref(false);
    const radioValue = ref('option1');
    const selectedFruit = ref('Die');
    const textareaText = ref('');
    const showEmoji = ref(false);
    const items = ref([]); // Define items if needed
    const watchedValue = ref(''); // Define watchedValue if needed

    // Computed properties
    const isActive = computed(() => count.value % 2 === 0);
    const textColor = computed(() => (count.value < 3 ? 'red' : 'blue'));
    const fontSize = ref(24);
    const arrayOfEmoji = computed(() => Array.from(new Array(count.value), () => props.emoji).join(''));

    // Event handling functions
    const increment = () => count.value++;
    const decrement = () => count.value--;
    const toggleEmoji = () => (showEmoji.value = !showEmoji.value);
    const inlineClickHandler = () => {
      // Handle inlineClickHandler if needed
    };

    // Watchers
    watch(inputText, (newInputText) => {
      textareaText.value = newInputText;
    });

    watch(count, (newCount) => {
      if (newCount === 5) console.log('You have clicked five times');
    });

    // Return data and functions
    return {
      count,
      inputText,
      inputCheckbox,
      radioValue,
      selectedFruit,
      textareaText,
      showEmoji,
      arrayOfEmoji,
      items,
      watchedValue,
      increment,
      decrement,
      isActive,
      textColor,
      fontSize,
      toggleEmoji,
      inlineClickHandler
    };
  }
};
</script>
