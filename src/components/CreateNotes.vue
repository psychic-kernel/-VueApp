<template>
    <main>
        <form id="stickyNoteForm" @submit="addNote()">
            <textarea id="todoInput" 
                v-model="newNote"
                style="border: none;"  
                cols="30" rows="10">
            </textarea>
            <input id="submitButton" class="submit-button" type="submit" value="Submit"/>
        </form>
       <ul id="todosDisplay">
            <li v-for="(note, index) in storedNotes" 
                :key="index.id" 
                :class="{'done': note.done }">
                {{ note.text }}
                <br>
                <input id="removeButton" class="remove-button" type="button"
                    value="Remove"
                    @click="deleteNote(note)"
                />
                <input id="editButton" class="edit-button" type="button" value="Edit"
                    @click="editNote(note)">
                <br>
            </li>
       </ul>
    </main>
</template>

<script>
import { ref, onMounted, watch } from 'vue';
export default { 
    setup(){ 

        const newNote = ref('');
        const hideCompleted = ref(false);
        const storedNotes = ref(JSON.parse(localStorage.getItem('storedNotes')) || []);


        watch(storedNotes, (newNote) => {
            localStorage.setItem('storedNotes', JSON.stringify(newNote));
        },{ deep: true});
        //Methods
        const addNote = () => {
        const newId = storedNotes.value.length > 0 ?
        storedNotes.value[storedNotes.value.length - 1].id + 1 : 
        1;
        storedNotes.value.push({id: newId, text: newNote.value, done: false});
        newNote.value = '';
        };
        const editNote = (index) => {
            storedNotes.value = storedNotes.value.map( t => {
                if(t.id === note.id){
                    t.done = !t.done;
                }
                return t;
            });
        }
        
        const deleteNote = (index) => {
            storedNotes.value = storedNotes.value.filter( t =>
            t !== index); 
        }
        return {newNote, hideCompleted, storedNotes, addNote, deleteNote, editNote };
    }
};


</script>
<style scoped>
form#stickyNoteForm {
    position: relative;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    margin-left: 5px;
    margin-right: auto;
    
    border: 1px solid gray;
    border-radius: 15px;

}
#submitButton {
    background-color: var(--color-primary);
    color: rgb(240, 255, 240);
    border: none;
    padding: 5px;
    margin: 5px;
    background-color: rgba(43, 204, 43, 0.259);
    border-radius: 5px;
    box-shadow: 0 0 1px 2px rgb(180, 255, 186, .23);


}
#removeButton {
    position: relative;
    border: none;
    color: rgb(255, 219, 219);
    background-color: rgba(255, 46, 46, 0.792);
    border-radius: 5px;
    padding: 5px;
    box-shadow: 0 0 1px 2px rgb(255, 200, 200, .23);

}
#editButton {
    position: relative;
    border: none;
    color: rgb(255, 219, 219);
    background-color: rgb(58, 117, 255);
    border-radius: 5px;
    padding: 5px;
    box-shadow: 0 0 1px 2px rgb(255, 200, 200, .23);


}
.done {
    text-decoration: line-through;
    list-style-type: circle;
}
#todoInput {
    border: none;
    padding: 5px;
    margin: 10px;
    border-radius: 5px;
    box-shadow: 0 0 1px 2px rgb(180, 255, 186, .23);
    resize: none;
}
#todosDisplay {
    color: var(--color-fire);
}

</style>
