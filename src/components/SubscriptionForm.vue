<template>
  <div class="Form">
    <h1>Lista de espera</h1>
    <form v-on:submit.prevent>
      <div class="ddd">
        <label>DDD * </label>
        <input type="text" v-model="ddd" required maxlength="2" minlength="2" />
      </div>

      <div class="phone">
        <label>Telefone * </label>
        <input
          type="text"
          v-model="phone"
          required
          maxlength="9"
          minlength="8"
        />
      </div>

      <div class="phoneType">
        <label>Tipo de Telefone * </label>
        <select v-model="phoneType" required>
          <option value="Celular">Celular</option>
          <option value="Residencial">Residencial</option>
          <option value="Comercial">Comercial</option>
          <option value="Trabalho">Trabalho</option>
        </select>
      </div>

      <div class="option1 option">
        <input
          type="radio"
          id="active"
          value="Ativo"
          v-model="isActive"
          required
          :class="isActive === 'Ativo' ? 'activeRadio' : 'inactiveRadio'"
        />
        <label for="active">Telefone ativo</label>
      </div>
      <div class="option2 option">
        <input
          type="radio"
          id="inactive"
          value="Inativo"
          v-model="isActive"
          :class="isActive === 'Inativo' ? 'activeRadio' : 'inactiveRadio'"
          required
        />
        <label for="inactive">Telefone inativo</label>
      </div>
      <div class="firstName">
        <label>Nome </label>
        <input type="text" v-model="name" maxlength="14" minlength="2" />
      </div>
      <div class="lastName">
        <label>Sobrenome </label>
        <input type="text" v-model="surname" maxlength="30" minlength="2" />
      </div>
      <div class="viewTable">
        <button v-on:click="$emit('displayTable', 'table')">Ver tabela</button>
      </div>
      <div class="addUser">
        <button
          v-on:click="
            $emit('addUser', {
              id: userJson.length + 1,
              name: name,
              surname: surname,
              ddd: ddd,
              phone: phone,
              phoneType: phoneType,
              active: isActive,
            })
          "
        >
          Adicionar
        </button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  props: {
    userJson: {
      type: Array,
    },
  },
  data() {
    return {
      ddd: "",
      phone: "",
      phoneType: "",
      isActive: "",
      name: "",
      surname: "",
      radioUrl: "../assets/radio-off.svg",
    };
  },
};
</script>

<style lang="scss">
.Form {
  color: $primaryWhite;
  font-weight: bold;
  height: 100%;
  display: flex;
  flex-direction: column;
  h1 {
    text-align: center;
  }
  form {
    display: grid;
    height: 100%;
    width: 90%;
    margin: 2% auto;
    grid-template-rows: 1fr 1fr 1fr 1fr;
    grid-template-columns: 0.4fr 1.5fr 1.5fr 0.8fr 0.8fr;
    grid-template-areas: "ddd phone phoneType option1 option2" "firstName firstName lastName lastName lastName" "addUser addUser addUser addUser addUser" "viewTable viewTable viewTable viewTable viewTable";
    grid-gap: 1.4rem;
    input,
    select {
      width: 100%;
      height: 50%;
      border: 1px solid #707070;
      font-size: 20px;
      padding: 0px 0px 0px 10px;
    }
    .ddd {
      grid-area: ddd;
    }
    .phone {
      grid-area: phone;
    }
    .phoneType {
      grid-area: phoneType;
    }
    .active {
      grid-area: selected;
    }
    .firstName {
      grid-area: firstName;
    }
    .lastName {
      grid-area: lastName;
    }
    .option1 {
      grid-area: option1;
    }
    .option2 {
      grid-area: option2;
    }

    .option {
      display: inline-flex;
      justify-content: start;
      align-items: center;
      width: 90%;
      white-space: nowrap;
      input {
        -webkit-appearance: none;
        cursor: pointer;
        outline: none;
        min-width: 30px;
        min-height: 30px;
        border: 0px;
      }
      label {
        cursor: pointer;
        font-size: $secondaryTextSize;
      }
    }
    .activeRadio {
      background: url("../assets/radio-on.svg") no-repeat left;
    }
    .inactiveRadio {
      background: url("../assets/radio-off.svg") no-repeat left;
    }
    .viewTable {
      grid-area: viewTable;
      display: flex;
      justify-content: center;
      button {
        color: $primaryWhite;
        background-color: $secondaryGray;
        border-radius: 9px;
        border: 0px;
        height: 60%;
        width: 25%;
      }
    }
    .addUser {
      grid-area: addUser;
      display: flex;
      justify-content: flex-end;
      button {
        color: $primaryWhite;
        background-color: $primaryOrange;
        border-radius: 9px;
        border: 0px;
        height: 60%;
        width: 18%;
      }
    }
  }
  label {
    color: $primaryWhite;
    font-size: $primaryTextSize;
  }

  @media only screen and (max-width: 950px) {
    form {
      grid-gap: 0px;
      grid-template-columns: 1fr;
      grid-template-rows: 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr;
      grid-template-areas: "ddd" "phone" "phoneType" "active" "option1" "option2" "firstName" "lastName" "viewTable" "addUser";
      input {
        padding: 0px;
      }
      input[type="radio"] {
        width: 10%;
      }
      .option label {
        font-size: $primaryTextSize;
      }
      .viewTable,
      .addUser {
        button {
          width: 100%;
          height: 100%;
        }
      }
    }
  }
}
</style>
