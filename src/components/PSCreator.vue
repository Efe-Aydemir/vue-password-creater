<template>
    <div class="mt-20">
        <div :class="copclass" class="bg-white text-4xl flex-wrap absolute inset-0 transition-all duration-500 flex justify-center items-center">Copied To Text Clipboard</div>
        <div class="gap-10 flex justify-center items-center flex-col">
            <h1 class="text-white p-5 flex justify-between w-52">
            <pre>{{value}}</pre>
            <pre v-if="copiedvalue === false" class='cursor-pointer' @click="copied">&#128203;</pre>
            <pre v-else >✅</pre>
        </h1>
        <button class="p-5 w-52 rounded-md text-bold text-xl bg-white" @click="password">Create Password</button>
        </div>    
    </div>
</template>

<script setup>
import {ref} from 'vue'

let copclass = ref('invisible opacity-0')
let copiedvalue = ref(false)
let value = ref('Empty')
let largeLetters = ref(['A','B','C','D','E','F','G','H','P','Z','T','Y'])
let letters = ref(['a','b','c','d','r','f','g','h','p','z','t','y'])
let numbers = ref([1,2,3,4,5,6,7,8,9])
let special = ref(['!','#','@','$','&','?','-','_'])


function copied() {
    copiedvalue.value = true
    navigator.clipboard.writeText(value.value)
    copclass.value = 'visible opacity-100'
    setTimeout(() => {
        copclass.value = 'invisible opacity-0'
    },1000)
}

function password() {
    copiedvalue.value = false
    value.value = ''
    if (value.value.length >= 12) {
        value.value = ''
    } else {
        for (var i = 0;i < 3;i++) {
        value.value += largeLetters.value[Math.floor(Math.random() * largeLetters.value.length)]
        for (var a = 0; a < 1;a++) {
            value.value += letters.value[Math.floor(Math.random() * letters.value.length)]
            for (var b = 0; b < 1; b++) {
                value.value += numbers.value[Math.floor(Math.random() * numbers.value.length)]
            }
            for (var c = 0; c < 1;c++) {
                value.value += special.value[Math.floor(Math.random() * special.value.length)]
            }
        }
    }
    }
}

</script>