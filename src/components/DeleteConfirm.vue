<template>
    <div class="delete-popup" v-if="isOpen">
      <div class="content">
        <h3>Confirmation</h3>
        <p>Are you sure you want to delete this tweet?</p>
        <div>
          <button @click="cancelDelete">Cancel</button>
          <button @click="confirmDelete">Delete</button>
        </div>
      </div>
    </div>
</template>

<script>
export default {
props: {
  isOpen: {
    type: Boolean,
    required: true,
  },
},
methods: {
  cancelDelete() {
    this.$emit('cancel');
  },
  confirmDelete() {
    this.$emit('confirm');
  },
},
};
</script>

<style scoped>
.delete-popup {
display: flex;
align-items: center;
justify-content: center;
position: fixed;
top: 0;
left: 0;
right: 0;
bottom: 0;
background-color: rgba(0, 0, 0, 0.5);
}

.content {
background-color: #fff;
padding: 20px;
border-radius: 8px;
max-width: 400px;
text-align: center;
}
</style>
  
