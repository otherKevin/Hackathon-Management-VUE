<template>
  <div class="tableau">
    <table>
      <thead>
        <tr>
          <th>Utilisateurs</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td class="td">Prénom</td>
          <td class="td">Nom</td>
          <td class="td">Email</td>
          <td class="td">Role</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style scoped>
table,
.td {
  border: 1px solid #333;
}

thead {
  background-color: #333;
  color: #fff;
}

.tableau {
  display: flex;
  justify-content: center;
  margin-top: 2%;
}
</style>
