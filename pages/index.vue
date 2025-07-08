<script setup >
import { NuxtLink } from '#components';
import { usePlayerName, usePlayerName2 } from '~/composables/state';

const response = await  useFetch('/api/hello');

console.log(response);

definePageMeta({
    layout: 'login',
})
const player1Name = ref('');
const player2Name = ref('');
const p1Name = usePlayerName();
const p2Name = usePlayerName2();

p1Name.value = player1Name;
p2Name.value = player2Name;
const canPlay = ref(false);
const submitName = () => {
    if(p1Name.value != "" && p2Name.value != "")
    {
        navigateTo("/game");
    }

}


</script>

<template>
    <NuxtLayout>
        <!-- <div>
        This is suppose to be the Login page!
        </div> -->

        
        <div>
            <h3>Player 1 Name - </h3>
            <UInput v-model="player1Name" color="neutral" highlight placeholder="Enter P1 Name..." />
        </div>

        <div>
            <h3>Player 2 Name - </h3>
            <UInput v-model="player2Name" color="neutral" highlight placeholder="Enter P2 Name..." />
        </div>

    <div >
      <UButton class="audioWide" @click.stop="submitName()">Let's Play</UButton>
    </div>

    </NuxtLayout>
   
</template>

<style>

.center {
  margin: auto;
  width: 100%;
  text-align: center;
}

</style>