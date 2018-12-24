<template>
  <div class="modal-backdrop" v-show="show">
    <div class="modalOpen card">
      <p class="text-center text-2xl font-bold mb-4">
        Are you sure you want to change the status for
        <strong>{{showName}}</strong>
        from
        <span>{{activeInactive}}</span> ?
      </p>

      <div class="text-center">
                <button @click="close" class="btn btn-secondary ml-4">Close</button>
        <button @click="dismiss" type="button" class="btn btn-primary ml-4">Change status</button>
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
    },
    close(){
      this.$emit("open", true);
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
  box-shadow: 0 14px 28px rgba(0, 0, 0, 0.25), 0 10px 10px rgba(0, 0, 0, 0.22);
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

span {
  color: blue;
}
</style>
