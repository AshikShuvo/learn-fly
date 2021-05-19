<template>
<base-dialog v-if="inputIsInvalid" title="Invalid Input" @close="closeDialog">
    <template #default>
        <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Recusandae pariatur itaque ex ipsa voluptatem ipsum reprehenderit asperiores quod doloribus deleniti.</p>
        <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Quibusdam, qui.</p>
    </template>
    <template #actions>
        <base-button @click="closeDialog">OK</base-button>
    </template>
</base-dialog>
  <base-card>
    <form @submit.prevent="submitData">
        <div class="form-control" >
            <label for='title'>Title</label>
            <input id="title" name='title' type="text" ref="titleInput"/>
        </div>
         <div class="form-control">
            <label for='description'>Description</label>
            <textarea id="description" name='description' rows='3' type="text" ref="descInput"/>
        </div>
         <div class="form-control">
            <label for='link'>Linf</label>
            <input id="link" name='link' type="url" ref="linkInput"/>
        </div>
        <base-button type="submit">Add Resource</base-button>
    </form>
  </base-card>
</template>

<script>


 

export default {
 inject:['addResource'],
 data(){
     return {
         inputIsInvalid:false
     }
 },
 methods:{
     submitData(){
         console.log('hitted')
         const title=this.$refs.titleInput.value;
         const description=this.$refs.descInput.value;
         const url=this.$refs.linkInput.value;

        if(title===''|| description===''||url===''){
            this.inputIsInvalid=true
            return ;

        }

        this.addResource(title,description,url)
     },
     closeDialog(){
         this.inputIsInvalid=false;
     }
 }

}
</script>

<style>
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