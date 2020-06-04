<template>
  <div>
    <p>ELEVATOR PANEL</p>
    <tbody>
      <tr v-for="floor in floors" :key="floor">
        <td>
          <b-button @click="callElevator(floor)">
            {{ floor }}
          </b-button>
        </td>
      </tr>
    </tbody>
    <b-row>
      <b-col>
        <b-button disabled="disabled">{{
          this.isSelectedFloorUp ? 'UP' : 'DOWN'
        }}</b-button>
      </b-col>
      <b-col>
        <b-button disabled="disabled">
          {{ this.isDoorOpen ? 'OPEN' : 'CLOSED' }}
        </b-button>
      </b-col>
    </b-row>
    <p>You are at floor : {{ currentFloor }}</p>
  </div>
</template>

<script>
export default {
  props: ['floors', 'currentFloor', 'isDoorOpen', 'isSelectedFloorUp'],
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
