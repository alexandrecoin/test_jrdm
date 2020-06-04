<template>
  <b-container class="bv-example-row">
    <b-row>
      <b-col><Building :floors="floors" :currentFloor="currentFloor"/></b-col>
      <b-col
        ><Panel
          :floors="floors"
          :currentFloor="currentFloor"
          :isDoorOpen="isDoorOpen"
          :isSelectedFloorUp="isSelectedFloorUp"
          @callElevator="changeFloor"
      /></b-col>
    </b-row>
  </b-container>
</template>

<script>
import Building from './Building';
import Panel from './Panel';

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
      isSelectedFloorUp: true,
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
      // console.log('2', floor, this.floor);
      this.currentFloor < floor
        ? (this.isSelectedFloorUp = true)
        : (this.isSelectedFloorUp = false);
      // console.log('isSelectedUp:', this.isSelectedFloorUp);
    },

    async changeFloor(floor) {
      // console.log('1', floor, this.currentFloor);
      this.checkFloorUpDown(floor);
      await this.handleDoors();
      await this.updateFloorState(floor);
      await this.handleDoors();
    },
  },
};
</script>
