<template>
  <div>
    <p>AFFICHAGE</p>
    <table>
      <tbody>
        <tr v-for="floor in floors" :key="floor">
          <td> {{ floor === 0 ? 'RDC' : floor }}</td>
          <td>
            <b-button :variant="floorColor(floor)" />
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  props: ['floors', 'currentFloor'],
  methods: {
    floorColor(floor) {
      return floor === this.currentFloor ? 'success' : 'danger';
    },
  },
};
</script>
