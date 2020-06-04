<template>
  <div>
    <table>
      <tbody>
        <tr v-for="floor in floors" :key="floor">
          <td>{{ floor }}</td>
          <td>
            <b-button/>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  props: ['floors'],
};
</script>
