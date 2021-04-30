<template>
<div>
      <!-- <BaseModal ref="BaseModal_ref">
    <div class="modal-delete-container">
      <div class="modal-delete">
        <div class="modal-delete-header"></div>
        <div class="modal-delete-content"></div>
        <div class="modal-delete-footer"></div>
      </div>
    </div>
  </BaseModal> -->
</div>
</template>

<script>
import BaseModal from "../BaseModalForm.vue";

export default {
  Components: {
    BaseModal,
  },
};
</script>


<style scoped>
.modal-delete-container {
  z-index: 1000;
 
  border-radius: 5px;
  position: absolute;
  top: calc(50% - 300px);
  left: calc(50% - 350px);
  border: 2px solid #e5e6e5;
}
.modal-delete {
  height: 156px;
  width: 400px;
  position: relative;
  background: red;
  border: 2px solid yellow;
}

.modal-delete-header {
  height: 20px;
  width: calc(396px - 28px);
  background: green;
  padding: 10px 16px;
}

.modal-delete-footer {
  height: 48px;
  background: yellow;
  bottom: 0px;
}

.modal-delete-content{
    height: calc(100% - 48px - 40px);
    
}
</style>