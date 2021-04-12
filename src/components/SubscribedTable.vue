<template>
  <div class="Table">
    <div class="tableContainer">
      <table>
        <tr>
          <th>Nome</th>
          <th>Sobrenome</th>
          <th>Telefone</th>
          <th>Tipo de telefone</th>
          <th>Status</th>
          <th></th>
        </tr>
        <tr
          v-for="subscribedUser in userJson"
          :key="subscribedUser.id"
          class="whatever"
        >
          <td>{{ subscribedUser.name }}</td>
          <td>{{ subscribedUser.surname }}</td>
          <td>
            ({{ subscribedUser.ddd }})
            {{ subscribedUser.phone.substring(0, 5) }}-{{
              subscribedUser.phone.substring(5, 9)
            }}
          </td>
          <td>{{ subscribedUser.phoneType }}</td>
          <td>{{ subscribedUser.active }}</td>
          <td class="remove" v-on:click="$event.path[1].remove()">X Excluir</td>
        </tr>
      </table>
    </div>
    <button class="navigateButton" v-on:click="$emit('displayForm', 'form')">
      Cadastrar
    </button>
  </div>
</template>

<script>
export default {
  props: ["userJson"],
};
</script>

<style lang="scss">
.Table {
  width: 100%;
  color: $primaryGray;
  display: flex;
  align-items: center;
  flex-direction: column;
  .tableContainer {
    height: 80%;
    width: 90%;
    display: block;
    overflow: auto;
  }
  .navigateButton {
    background-color: $primaryOrange;
    color: $primaryWhite;
    border: 0px;
    border-radius: 9px;
    width: 20%;
    padding: 1% 1%;
    margin: 10% 0px;
  }
  table {
    height: 100%;
    border-top: 0px;
    font-size: 16px;
    border-spacing: 0px;
    text-align: left;
    th,
    td {
      padding-left: 10px;
    }
    th {
      color: $primaryWhite;
      font-size: 20px;
      height: 45px;
      background-color: $primaryBlack;
      border: 0px solid $primaryBlack;
    }
    tr {
      width: 100%;
      background-color: $primaryWhite;
    }
    tr:nth-child(4n),
    tr:nth-child(4n + 2) {
      background-color: $secondaryWhite;
    }
    td {
      height: 30px;
    }
    .remove {
      color: $primaryOrange;
      cursor: pointer;
    }
  }
}

@media only screen and (max-width: 950px) {
  .Table {
    .navigateButton {
      padding: 5vw;
      width: 100%;
      max-height: 50px;
    }
  }
}
</style>
