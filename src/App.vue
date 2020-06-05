<template>
  <b-container id="app" class="bv-example-row">
    <b-row>
      <b-col><Building :floors="floors" :currentFloor="currentFloor"/></b-col>
      <b-col
        ><Panel
          :floors="floors"
          :currentFloor="currentFloor"
          :isDoorOpen="isDoorOpen"
          :elevatorDirection="elevatorDirection"
          @callElevator="changeFloor"
      /></b-col>
    </b-row>
  </b-container>
</template>

<script>
import Building from './components/Building';
import Panel from './components/Panel';

export default {
  name: 'Container',
  components: {
    Building,
    Panel,
  },
  data() {
    return {
      floors: [6, 5, 4, 3, 2, 1, 0],
      currentFloor: 0,
      isDoorOpen: true,
      elevatorDirection: '',
    };
  },
  methods: {
    handleDoors() {
      return new Promise((resolve) => {
        setTimeout(() => {
          this.isDoorOpen = !this.isDoorOpen;
          resolve('Open / Closed');
        }, 1000);
      });
    },

    updateFloorState(floor) {
      return new Promise((resolve) => {
        setTimeout(() => {
          this.currentFloor = floor;
          console.log(this.currentFloor);
          resolve('Floor updated');
        }, 2000);
      });
    },

    checkFloorUpDown(floor) {
      this.currentFloor < floor
        ? (this.elevatorDirection = 'up')
        : this.currentFloor > floor
        ? (this.elevatorDirection = 'down')
        : (this.elevatorDirection = 'same');
    },

    async changeFloor(floor) {
      this.checkFloorUpDown(floor);
      if (this.elevatorDirection !== 'same') {
        await this.handleDoors();
        await this.updateFloorState(floor);
        await this.handleDoors();
      }
    },
  },
};
</script>
