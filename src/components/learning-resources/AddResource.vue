<template>
    <h2>Add Resources</h2>
    <base-dialog v-if="inputIsInvalid" title="Invalid Input" @closeDialog="confirmError">
        <!-- <template #header>
            <p>Invalid!</p>
        </template> -->
        <template #default>
            <p>At least one input is invalid!</p>
        </template>
        <template #buttonActions>
            <base-button @click="confirmError">Okay</base-button>
        </template>
    </base-dialog>
    <base-card>
        <form @submit.prevent="submitAddNewResource">
            <div class="form-control">
                <label for="title">Title</label>
                <input type="text" id="title" name="title" v-model.trim="title" ref="titleInput">    
            </div>
            <div class="form-control">
                <label for="description">Description</label>
                <textarea type="text" id="description" name="description" v-model.trim="description" ref="descriptionInput"></textarea>   
            </div>
            <div class="form-control">
                <label for="link">Resource Link</label>
                <input type="url" id="link" name="link" v-model.trim="urlLink" ref="linkInput">    
            </div>
            <div>
                <base-button type="submit">Add New Resource</base-button>
            </div>
        </form>
    </base-card>
</template>

<script>
import BaseButton from '../UI/BaseButton.vue';
export default {
  components: { BaseButton },
    data() {
        return {
            title: "",
            description: "",
            urlLink: "",
            inputIsInvalid: false
        };
    },
    inject: ["addNewResource"],
    methods: {
        submitAddNewResource() {
            const titleInput = this.$refs.titleInput.value;
            const descriptionInput = this.$refs.descriptionInput.value;
            const linkInput = this.$refs.linkInput.value;

            if(titleInput === "" || descriptionInput === "" || linkInput === ""){
                this.inputIsInvalid = true;
                return;
            }

            //assuming not empty
            this.addNewResource(titleInput, descriptionInput, linkInput);

                    //why is this highlighted red and giving undefined
                    // this.title = event.target.value;
                    // console.log(this.title);
        },
        // addNewResource(title, description, urlLink) {
            //I had the right idea with this method but I implemented it in the wrong place. This should be in the parent where the data is actually stored and called from child. Hence I dont have to inject resources but the add resources method
        //     const newResource = {
        //         id: new Date().toISOString(),
        //         title: title,
        //         description: description,
        //         urlLink: urlLink

        //     }
        //     this.resources.push(newResource);
        // },
        confirmError () {
            this.inputIsInvalid = false;
        }
    }
}
</script>

<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>