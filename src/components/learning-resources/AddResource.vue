<template>
    <base-dialog v-if="inputIsInvalid" title="Invalid input" @close="confirmError">
        <template #default>
            <p>Your input value is invalid.</p>
            <p>Please check your inputs.</p>
        </template>
        <template #actions>
            <base-button @click="confirmError">Okey</base-button>
        </template>
    </base-dialog>
  <base-card>
    <form @submit.prevent="submitData">
      <div class="form-control">
        <label for="title">Title</label>
        <input type="text" id="title" name="title" v-model="title" />
      </div>

      <div class="form-control">
        <label for="description">Description</label>
        <textarea name="description" id="description" rows="3" v-model="desc"></textarea>
      </div>

      <div class="form-control">
        <label for="link">Link</label>
        <input type="url" id="link" name="link" v-model="link" />
      </div>

      <base-button type="submit">Add Resource</base-button>
    </form>
  </base-card>
</template>

<script>
export default {
    inject: ['addResource'],
    data(){
        return{
            title: '',
            desc: '',
            link: '',
            inputIsInvalid: false
        }
    },
    methods:{
        submitData(){
            if(this.title.trim() === '' || this.desc.trim() === '' || this.link.trim() === ''){
                this.inputIsInvalid = true
                return;
            }
            this.addResource(this.title,this.desc,this.link)
        },
        confirmError(){
            this.inputIsInvalid = false
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