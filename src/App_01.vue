<script setup>
// import HelloWorld from './components/HelloWorld.vue'
// import TheWelcome from './components/TheWelcome.vue'

import { ref } from 'vue'
import { reactive } from 'vue'
const showMore = ref(false)
const count = ref(0)
const showModal = ref(false)
const awesome = ref(false)
// const items = ref([{ message: 'Foo'},{ message: 'Bar'}]);
// const parentMessage = ref('Parent')


const myObject = reactive ({
  title: 'How to do lists in Vue',
  author: 'Jane Doe',
  publishedAt: '2016-04-10'
})

function increaseCounter() {
  count.value++
}

function degreaseCounter() {
  count.value--
}

function toggleMore() {
  showMore.value = !showMore.value
}
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />
    </div>
  </header>

  <main>
    <p>Lorem ipsum dolor sit amet
    <template v-if="!showMore">...</template>
    <template v-else>
      Lorem ipsum dolor sit amet consectetur adipisicing elit. Nisi, ut doloremque. Ipsa, minima,
      magnam perferendis incidunt repellat sit vitae esse ratione, earum ut fugiat iusto veniam
      excepturi reiciendis sed commodi modi iure qui cum eius molestias? Natus quod accusantium
      ipsam, laboriosam delectus ipsa, rem eum recusandae, at maiores velit officia obcaecati. Eum
      numquam sed placeat officia, porro eius reprehenderit sapiente odio, nihil quia ex blanditiis
      quos explicabo optio soluta natus in neque dolorem autem quidem nam consequatur unde aliquid
      enim. Culpa totam animi blanditiis iusto, illo voluptatibus tempore, aspernatur corrupti fuga
      harum deleniti aperiam tenetur, molestias quos nobis inventore possimus.
    </template>
    </p>
    <button @click="toggleMore">{{ showMore ? 'Mniej' : 'Więcej' }}</button>
    <p>counter {{ count }}</p>
    <button @click="increaseCounter">zwwiększ</button>
    <button @click="degreaseCounter">zmniejsz</button>
    <hr />
    <button @click="showModal = true">Just Do it</button>
    <div class="modal" v-if="showModal">
      Tekst do wyświetlenia w modalu <button @click="showModal = false">zamknij się</button>
    </div>
    <hr />
    <button @click="awesome = !awesome">Toggle</button>
<h1 v-if="awesome">Vue is awesome!</h1>
<h1 v-else>Oh no 😢</h1>
<hr>
<li v-for="item in items">
{{ item.message  }}
</li> 
<li v-for="(item, index) in items">
{{  parentMessage  }} - {{  index }} - {{ item.message }}
</li>
<hr>
<ul>
  <li v-for="(value, key, index) in myObject">
    {{ index }},  {{ key }} :{{ value }}
  </li>
</ul>
<hr>






  </main>

  <!-- <main>
    <TheWelcome />
  </main> -->
</template>

<style scoped>
.modal {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 300px;
  height: 100px;
  background: grey;
  color: #fff;
}

/* header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
} */

/* @media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
} */
</style>
