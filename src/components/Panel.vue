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
        <b-button disabled="disabled">SENS : {{ elevatorDirection }}</b-button>
      </b-col>
      <b-col>
        <b-button disabled="disabled">
          {{ doorsState }}
        </b-button>
      </b-col>
    </b-row>
    <p>Vous êtes à l'étage : {{ currentFloor }}</p>
  </div>
</template>

<script>
export default {
  props: ['floors', 'currentFloor', 'isDoorOpen', 'isSelectedFloorUp'],
  computed: {
    elevatorDirection() {
      return this.isSelectedFloorUp ? 'MONTÉE' : 'DESCENTE';
    },
    doorsState() {
      return this.isDoorOpen ? 'PORTES OUVERTES' : 'PORTES FERMÉES';
    },
  },
  data() {
    return {
      disabled: true,
    };
  },
  methods: {
    callElevator(floor) {
      this.$emit('callElevator', floor);
    },
  },
};
</script>