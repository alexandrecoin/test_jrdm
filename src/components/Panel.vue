<template>
  <div>
    <p>PANNEAU ASCENSEUR</p>
    <tbody>
      <tr v-for="floor in floors" :key="floor">
        <td>
          <b-button pill @click="callElevator(floor)" class="mb-1">
            {{ floor === 0 ? 'RDC' : floor }}
          </b-button>
        </td>
      </tr>
    </tbody>
    <b-row>
      <b-col>
        <b-button disabled>SENS : {{ elevatorOrientation }}</b-button>
      </b-col>
      <b-col>
        <b-button disabled>
          {{ doorsState }}
        </b-button>
      </b-col>
    </b-row>
    <p>Vous êtes à l'étage : {{ currentFloor }}</p>
  </div>
</template>

<script>
export default {
  props: ['floors', 'currentFloor', 'isDoorOpen', 'elevatorDirection'],
  computed: {
    elevatorOrientation() {
      return this.elevatorDirection === 'up'
        ? 'MONTÉE'
        : this.elevatorDirection === 'down'
        ? 'DESCENTE'
        : 'AUCUN DÉPLACEMENT';
    },
    doorsState() {
      return this.isDoorOpen ? 'PORTES OUVERTES' : 'PORTES FERMÉES';
    },
  },
  methods: {
    callElevator(floor) {
      this.$emit('callElevator', floor);
    },
  },
};
</script>
