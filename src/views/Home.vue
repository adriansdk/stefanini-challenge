<template>
  <div :class="formActive ? 'form-bg' : 'table-bg'">
    <div :class="formActive ? 'form-logo' : 'table-logo'">
      <img alt="blackwall-logo" src="../assets/blackwall-sub.svg" />
    </div>
    <div :class="formActive ? 'form-container' : 'table-container'">
      <div v-if="formActive" class="form">
        <subscription-form
          v-on:addUser="addSubscriber"
          v-on:displayTable="handleScene"
          :userJson="subscribedUsers"
        />
      </div>
      <div v-if="tableActive" class="table">
        <subscribed-table
          :userJson="subscribedUsers"
          v-on:displayForm="handleScene"
          v-on:removeUser="removeSubscriber"
        />
      </div>
    </div>
  </div>
</template>

<script>
import SubscriptionForm from "../components/SubscriptionForm";
import SubscribedTable from "../components/SubscribedTable.vue";
import userSeed from "../seed.json";

export default {
  name: "Home",
  components: {
    SubscriptionForm,
    SubscribedTable,
  },
  data() {
    return {
      subscribedUsers: [...userSeed],
      formActive: true,
      tableActive: false,
    };
  },
  methods: {
    addSubscriber: function (subscriber) {
      console.log(subscriber);
      this.subscribedUsers.push(subscriber);
    },
    handleScene: function (activeScene) {
      if (activeScene === "table") {
        this.formActive = false;
        this.tableActive = true;
      } else if (activeScene === "form") {
        this.formActive = true;
        this.tableActive = false;
      }
    },
  },
};
</script>

<style lang="scss">
.form-bg {
  display: flex;
  flex-direction: column;
  justify-content: center;
  height: 100vh;
  background-image: url("../assets/coffee-bg.png");
  background-size: cover;
  background-position: top;
  .form-container {
    height: 70%;
    width: 80%;
    margin: auto;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    background: transparent;
    backdrop-filter: blur(14px);
    border-radius: 41px;
  }
  .form {
    height: 100%;
  }
  .form-logo {
    align-self: flex-end;
    margin: 5% 7% 0 0;
    img {
      height: 8vw;
      min-height: 100px;
    }
  }
}
.table-bg {
  background-image: url("../assets/table-bg.png");
  background-size: cover;
  background-position: top;
  height: 100vh;
  table {
    width: 100%;
  }
  .table-container {
    height: 80%;
    width: 85%;
    margin: 5% auto 0%;
  }
  .table-logo {
    align-self: flex-start;
    width: 100%;
    background-color: $primaryBlack;
    img {
      height: 4vw;
      margin: 0 0 1% 2%;
      min-height: 100px;
    }
  }
}
</style>
