<template>
    <div>
        <h1>flight tracker {{ fdat.td_id_fltdata_departure_baggage_id }} to {{ fdat.td_id_fltdata_destination_baggage_id }}</h1>
        <p>O2 present: {{ !!fdat.td_id_decompression }}</p>
        <p>in flight: {{ !!fdat.td_id_weight_on_wheels }}</p>
        <p>altitude: {{ fdat.td_id_fltdata_altitude }} ft</p>
        <p>distance from origin: {{ fdat.td_id_fltdata_distance_from_origin }} miles</p>
        <p>distance to destination: {{ fdat.td_id_fltdata_distance_to_destination }} miles</p>
        <p>ground speed: {{ fdat.td_id_fltdata_ground_speed }} km/h</p>
        <p>headwind speed: {{ fdat.td_id_fltdata_head_wind_speed }} km/h</p>
        <p>curr heading: {{ fdat.td_id_fltdata_true_heading }} deg</p>
        <p>current lat: {{ fdat.td_id_fltdata_present_position_latitude }} lat</p>
        <p>current lng: {{ fdat.td_id_fltdata_present_position_longitude }} lng</p>
    </div>
</template>

<script>
  export default {
    name: "PanasonicAvionicsTracker",
    data() { return { fdat: {} } },
    created() { this.getFDat() },
    methods: {
        getFDat: function() {
          setInterval(() => {
            fetch("http://services.inflightpanasonic.aero/inflight/services/flightdata/v1/flightdata")
            .then(res => res.json())
            .then(res => {this.fdat = res})
          }, 2000)
        }
    }
  }
</script>
