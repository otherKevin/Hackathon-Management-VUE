<template>
  <div class="tableau">
    <table>
      <tbody>
        <tr>
          <td>{{ firstname }}</td>
          <td>{{ lastname }}</td>
          <td>{{ email }}</td>
          <!-- <td>
            <router-link
              :to="{
                name: 'Profil',
                params: {
                  user_id: this.user_id,
                },
              }"
            >
              <button class="showBtn">Profil</button>
            </router-link>
          </td> -->
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  props: {
    firstname: String,
    lastname: String,
    email: String,
    user_id: Number,
  },
};
</script>

<style scoped>
table,
.td {
  border: 1px solid #333;
}

.tableau {
  display: flex;
  justify-content: center;
}
</style>
