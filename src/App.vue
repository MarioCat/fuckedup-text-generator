<script setup>
  import { onMounted, ref } from "@vue/runtime-core";

  onMounted(() => document.title = "f u C kE d    u P   t e X t   Ge N e ra tor");

  const inputText = ref("");
  const generatedText = ref();
  const tooltip = ref();

  const generateRandomBoolean = () => Math.floor(Math.random() * 2);

  const generateRandomNumberOfSpaces = (maxNumberOfSpaces) => Math.floor(Math.random() * maxNumberOfSpaces);

  const convertToFuckedUpText = (text) => {
    const splittedText = text.split('');
    const space = ' ';

    return splittedText.map(letter => {
      let setToUpperCase = generateRandomBoolean();
      let numberOfSpaces = generateRandomNumberOfSpaces(5);

      return setToUpperCase ? `${letter.toUpperCase()}${space.repeat(numberOfSpaces)}` : `${letter}${space.repeat(numberOfSpaces)}`;
    })
    .join('');
  };

  const handleClick = () => {
    const textCopied = generatedText.value.innerText;
    navigator.clipboard.writeText(textCopied);
    tooltip.value.innerText = "Copied !";
  };

  const resetTooltipText = () => tooltip.value.innerText = "Copy to clipboard";

</script>

<template>
  <div class="flex items-center justify-center w-full h-screen">
    
    <img class="z-0 top-0 absolute object-cover opacity-[0.7] w-full h-screen" src="./assets/background.jpg">
    
    <div class="flex flex-col items-center z-[1] w-1/2">
      <h1 class="text-4xl font-bold">f U  c K ed Up te x T gEn e R a T oR</h1>
      
      <input class="w-full p-4 my-4 rounded-full outline-none" type="text" v-model="inputText" placeholder="Input text"/>

      <h3 class="text-xl font-bold">g En E r A t e D te X t</h3>
      <div class="flex flex-row items-center px-4 py-3 bg-white rounded-full w-full justify-between">
        <p ref="generatedText" class="whitespace-pre truncate">{{ convertToFuckedUpText(inputText) }}</p>
        <div class="tooltip">
          <span ref="tooltip" class="tooltiptext">Copy to clipboard</span>
          <span 
            class="ml-4 px-2 py-1 text-sm rounded-full border-2 border-gray-300 cursor-pointer hover:bg-orange-500 hover:text-white"
            @click="handleClick"
            @mouseout="resetTooltipText">
            Copy
          </span>
        </div>
      </div>
    </div>

  </div>
</template>

<style>
.tooltip {
  position: relative;
  display: inline-block;
}

.tooltip .tooltiptext {
  visibility: hidden;
  width: 140px;
  background-color: #555;
  color: #fff;
  text-align: center;
  border-radius: 6px;
  padding: 5px;
  position: absolute;
  z-index: 1;
  bottom: 150%;
  left: 50%;
  margin-left: -65px;
  opacity: 0;
  transition: opacity 0.3s;
}

.tooltip .tooltiptext::after {
  content: "";
  position: absolute;
  top: 100%;
  left: 50%;
  margin-left: -5px;
  border-width: 5px;
  border-style: solid;
  border-color: #555 transparent transparent transparent;
}

.tooltip:hover .tooltiptext {
  visibility: visible;
  opacity: 1;
}
</style>