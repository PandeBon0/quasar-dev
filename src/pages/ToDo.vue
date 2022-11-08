<template>
  <q-page class="bg-grey-2 column">
    <div class="row q-pa-sm bg-primary">
      <q-input
        @keyup.enter="addElement()"
        class="col"
        square
        filled
        bg-color="white"
        v-model="newTaskText"
        placeholder="Agregar elemento"
        dense
      >
        <template v-slot:append>
          <q-btn
            @click="addElement()"
            round
            dense
            flat
            icon="add" />
        </template>
      </q-input>
    </div>

    <!-- <q-list
      class="bg-white"
      separator
      bordered
    >


      <q-item
        v-if="isQuasarDeleted === false"
        v-ripple
        @click="doneQuasar = !doneQuasar"
        clickable
        :class="{ 'done bg-blue-1' : doneQuasar}"
      >
        <q-item-section avatar>
          <q-checkbox
            v-model="doneQuasar"
            color="primary"
            class="no-pointer-events"
          />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{titleQuasar}}</q-item-label>
        </q-item-section>
        <q-item-section v-if="doneQuasar" side>
          <q-btn @click.stop="deleteQuasar()" flat round dense  color="primary" icon="delete" />
        </q-item-section>
      </q-item>

      <q-item
        v-if="areStylesDeleted === false"
        v-ripple
        @click="doneStyles = !doneStyles"
        clickable
        :class="{ 'done bg-blue-1' : doneStyles}"
      >
        <q-item-section avatar>
          <q-checkbox
            v-model="doneStyles"
            color="primary"
            class="no-pointer-events"
          />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{titleStyles}}</q-item-label>
        </q-item-section>
        <q-item-section v-if="doneStyles" side>
          <q-btn @click.stop="deleteStyles()" flat round dense  color="primary" icon="delete" />
        </q-item-section>
      </q-item>

      <q-item
        v-if="isDeleted === false"
        v-ripple
        @click="doneMeeting = !doneMeeting"
        clickable
        :class="{ 'done bg-blue-1' : doneMeeting}"
      >
        <q-item-section avatar>
          <q-checkbox
            v-model="doneMeeting"
            color="primary"
            class="no-pointer-events"
          />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{titleMeeting}}</q-item-label>
        </q-item-section>
        <q-item-section v-if="doneMeeting" side>
          <q-btn @click.stop="deleteTask()" flat round dense  color="primary" icon="delete" />
        </q-item-section>
      </q-item>

    </q-list> -->


    <q-list
      v-for="task in tasks "
      :key="task.title"
      class="bg-white"
      separator
      bordered
    >


      <q-item
        v-if="isTaskDeleted === false"
        v-ripple
        @click="task.done = !task.done"
        clickable
        :class="{ 'done bg-blue-1' : task.done}"
      >
        <q-item-section avatar>
          <q-checkbox
            v-model="task.done"
            color="primary"
            class="no-pointer-events"
          />
        </q-item-section>
        <q-item-section>
          <q-item-label>{{task.title}}</q-item-label>
        </q-item-section>
        <q-item-section v-if="task.done" side>
          <q-btn @click.stop="deleteTask()" flat round dense  color="primary" icon="delete" />
        </q-item-section>
      </q-item>



    </q-list>

  </q-page>
</template>

<script setup lang="ts">
import { Todo, Meta } from 'components/models';
import ExampleComponent from 'components/ExampleComponent.vue';
import { ref } from 'vue';
import Quasar, { useQuasar } from 'quasar';

var newTaskText = '';

// const titleQuasar = 'Iniciar curso quasar';
// var doneQuasar = ref(false);

// const titleStyles = 'Aplicar Estilos';
// var doneStyles = ref(false);

// const titleMeeting = 'Reunion';
// var doneMeeting = ref(false);

// var isQuasarDeleted = ref(false);
// var areStylesDeleted = ref(false);
// var isDeleted = ref(false);
var isTaskDeleted = ref(false);

const $q = useQuasar ();

const tasks = [
  {
    title: 'Iniciar curso Quasar',
    done: false
  }
]

// function deleteQuasar  ()  {
//   $q.dialog({
//     title: 'Confirm',
//     message: 'Eliminar elemento de la lista?',
//     cancel: true,
//     persistent: true
//   }).onOk(() => {
//     isQuasarDeleted.value = true;
//     $q.notify('Elemento eliminado')
//   })
//   return isDeleted
// }
// function deleteStyles  ()  {
//   $q.dialog({
//     title: 'Confirm',
//     message: 'Eliminar elemento de la lista?',
//     cancel: true,
//     persistent: true
//   }).onOk(() => {
//     areStylesDeleted.value = true;
//     $q.notify('Elemento eliminado')
//   })
//   return isDeleted
// }
function deleteTask  ()  {
  $q.dialog({
    title: 'Confirm',
    message: 'Eliminar elemento de la lista?',
    cancel: true,
    persistent: true
  }).onOk(() => {
    isTaskDeleted.value = true;
    $q.notify('Elemento eliminado')
  })
  return isTaskDeleted
}

function addElement () {
  tasks.push({
    title:  newTaskText,
    done: false
  })
}



//  function sendElement () {
//    var titleTask = newTaskText;
//    var doneTask = ref(false);
//    console.log(titleTask.value, doneTask.value)
//    return {titleTask, doneTask}
//    newTaskText.value = ''
//  }



</script>

<style lang="scss">
  .done {
    .q-item__label {
      text-decoration: line-through;
      color: #bbb;
    }
  }

</style>
