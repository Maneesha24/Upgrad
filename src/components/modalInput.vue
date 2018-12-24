<template>
  <div class="modal-backdrop" v-show="show">
    <div class="modalOpen card">
      <p class="text-center text-2xl font-bold mb-4">Are you sure you want to change the status for
        <strong>{{showName}}</strong>
        from {{activeInactive}} ?
      </p>

      <div class="text-center">
        <button @click="dismiss" type="button" class="btn btn-primary ml-4">Are you Sure?</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["show", "sendName", "active2Inactive"],

  methods: {
    dismiss() {
      this.$emit("close", true);
    }
  },
  updated() {
    if (!this.active2Inactive) {
      this.activeInactive = "Active to Inactive";
    } else {
      this.activeInactive = "Inactive to Active";
    }
  },
  data() {
    return {
      showName: this.sendName,
      activeInactive: ""
    };
  }
};
</script>

<style scoped>
.modal-backdrop {
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  overflow: auto;
  padding: 2rem;
  background-color: rgba(0, 0, 0, 0.5);
}
.modalOpen {
  margin-left: auto;
  margin-right: auto;
  max-width: 30rem;
  margin-top: 4rem;
}
.card,
.modalOpen {
  background-color: #fff;
  border-radius: 0.25rem;
  padding: 2rem;
  -webkit-box-shadow: 0 15px 30px 0 rgba(0, 0, 0, 0.11),
    0 5px 15px 0 rgba(0, 0, 0, 0.08);
  box-shadow: 0 15px 30px 0 rgba(0, 0, 0, 0.11),
    0 5px 15px 0 rgba(0, 0, 0, 0.08);
}

.btn-blue {
  background-color: red;
}

p {
  font-size: 1.2rem;
}

strong {
  color: red;
}
</style>
