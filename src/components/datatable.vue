<template>
  <section>
    <b-collapse class="card" animation="slide" aria-id="contentIdForA11y3" v-if="isMobile">
      <template #trigger="props">
        <div
            class="card-header"
            role="button"
            aria-controls="contentIdForA11y3">
          <p class="card-header-title">
            Filters
          </p>
          <a class="card-header-icon">
            <b-icon
                :icon="props.open ? 'angle-down' : 'angle-up'">
            </b-icon>
          </a>
        </div>
      </template>

      <div class="card-content">
        <div class="content">
          <b-field label="PSAP Name">
            <b-input v-model="searchMobile.PSAP_Name"></b-input>
          </b-field>
          <b-field label="City">
            <b-input v-model="searchMobile.City"></b-input>
          </b-field>
          <b-field label="County">
            <b-input v-model="searchMobile.County"></b-input>
          </b-field>
          <b-field label="State">
            <b-select v-model="searchMobile.State">
              <option
                  v-for="state in states"
                  :value="state.value"
                  :key="state.value">
                {{ state.text }}
              </option>
            </b-select>
          </b-field>
          <b-field label="ZIP">
            <b-input v-model="searchMobile.Zip" type="number" max="5"></b-input>
          </b-field>
          <b-field>
            <b-checkbox v-model="searchMobile.TTY">
              <label>Text to TTY</label>
            </b-checkbox>
          </b-field>
          <b-field>
            <b-checkbox v-model="searchMobile.Web_Browser">
              <label>Web Browser</label>
            </b-checkbox>
          </b-field>
          <b-field>
            <b-checkbox v-model="searchMobile.DirectIP">
              <label>Direct IP</label>
            </b-checkbox>
          </b-field>
          <b-field>
            <b-checkbox v-model="searchMobile.RTT">
              <label>RTT</label>
            </b-checkbox>
          </b-field>
        </div>
      </div>
      <footer class="card-footer">
        <b-button class="card-footer-item is-danger is-outlined" @click="reset">Reset</b-button>
        <b-button class="card-footer-item is-primary is-outlined" @click="filterMobile()">Search</b-button>
      </footer>
    </b-collapse>

    <div class="has-text-weight-bold mt-2" v-if="isMobile">
      Sort
    </div>
    <b-table
        :data="filterOn? dataFiltered : data"
        default-sort="PSAP_Name"
        paginated
        striped
        :per-page="isMobile ? 5 : 10"
        aria-next-label="Next page"
        aria-previous-label="Previous page"
        aria-page-label="Page"
        aria-current-label="Current page">
      <b-table-column field="PSAP_Name" label="PSAP Name" searchable sortable>
        <template v-slot:header>
          <b-tooltip label="Public Safety Answering Point" append-to-body dashed position="is-right">
            PSAP
          </b-tooltip>
          Name
        </template>
        <template v-slot="props">
          {{ props.row.PSAP_Name }}
        </template>
      </b-table-column>
      <b-table-column field="City" label="City" searchable sortable v-slot="props">
        {{ props.row.City }}
      </b-table-column>
      <b-table-column field="County" label="County" searchable sortable v-slot="props">
        {{ props.row.County }}
      </b-table-column>
      <b-table-column field="State" label="State" width="3em" searchable sortable v-slot="props">
        {{ props.row.State }}
      </b-table-column>
      <b-table-column field="Zip" label="ZIP" width="5em" numeric searchable sortable v-slot="props">
        {{ props.row.Zip }}
      </b-table-column>
      <b-table-column field="TTY" label="Text" searchable :custom-search="filterTable('TTY')" >
        <template v-slot:header>
          Text-to-
          <b-tooltip label="Text Telephone" append-to-body dashed>
            TTY
          </b-tooltip>
        </template>
        <template v-slot:searchable="props">
          <div class="vertical-align-middle">
            <b-checkbox v-model="props.filters['TTY']"></b-checkbox>
          </div>
        </template>
        <template v-slot="props">
          <b-icon
              icon="check"
              type="is-success"
              v-if="props.row.TTY === 1 || props.row.TTY === '1'">
          </b-icon>
          <b-icon
              icon="times"
              type="is-danger"
              v-else>
          </b-icon>
        </template>
      </b-table-column>
      <b-table-column field="Web_Browser" label="Web Browser" searchable :custom-search="filterTable('Web_Browser')" >
        <template v-slot:searchable="props">
          <div class="vertical-align-middle">
            <b-checkbox v-model="props.filters['Web_Browser']"></b-checkbox>
          </div>
        </template>
        <template v-slot="props">
          <b-icon
              icon="check"
              type="is-success"
              v-if="props.row.Web_Browser === 1 || props.row.Web_Browser === '1'">
          </b-icon>
          <b-icon
              icon="times"
              type="is-danger"
              v-else>
          </b-icon>
        </template>
      </b-table-column>
      <b-table-column field="DirectIP" label="Direct IP" searchable :custom-search="filterTable('DirectIP')" >
        <template v-slot:searchable="props">
          <div class="vertical-align-middle">
            <b-checkbox v-model="props.filters['DirectIP']"></b-checkbox>
          </div>
        </template>
        <template v-slot="props">
          <b-icon
              icon="check"
              type="is-success"
              v-if="props.row.DirectIP === 1 || props.row.DirectIP === '1'">
          </b-icon>
          <b-icon
              icon="times"
              type="is-danger"
              v-else>
          </b-icon>
        </template>

      </b-table-column>
      <b-table-column field="RTT" label="RTT" searchable :custom-search="filterTable('RTT')" >
        <template v-slot:header>
          <b-tooltip label="Real Time Text" append-to-body dashed>
            RTT
          </b-tooltip>
        </template>
        <template v-slot:searchable="props">
          <div class="vertical-align-middle">
            <b-checkbox v-model="props.filters['RTT']"></b-checkbox>
          </div>
        </template>
        <template v-slot="props">
          <b-icon
              icon="check"
              type="is-success"
              v-if="props.row.RTT === 1 || props.row.RTT === '1'">
          </b-icon>
          <b-icon
              icon="times"
              type="is-danger"
              v-else>
          </b-icon>
        </template>
      </b-table-column>
      <b-table-column field="Other" label="Other" sortable v-slot="props">
        <b-icon
            icon="check"
            type="is-success"
            v-if="props.row.Other === 1 || props.row.Other === '1'">
        </b-icon>
        <span v-else>
          {{ props.row.Other }}
        </span>
      </b-table-column>
      <template v-if="data.length < 1" #empty>
        <div class="has-text-centered">No records</div>
      </template>
    </b-table>
  </section>
</template>

<script>
const data = require( '../assets/text_911_master_psap_registry.json');

export default {
  props:{
    isMobile: Boolean
  },
  data() {
    return {
      name: 'datatable',
      data: data,
      dataFiltered: [],
      filterOn: false,
      searchMobile:{
        PSAP_Name: '',
        County: '',
        City: '',
        State: '',
        Zip: '',
        TTY: false,
        Web_Browser: false,
        DirectIP: false,
        RTT: false
      },
      states: [
        {
          text: "Alabama",
          value: "AL"
        },
        {
          text: "Alaska",
          value: "AK"
        },
        {
          text: "Arizona",
          value: "AZ"
        },
        {
          text: "Arkansas",
          value: "AR"
        },
        {
          text: "California",
          value: "CA"
        },
        {
          text: "Colorado",
          value: "CO"
        },
        {
          text: "Connecticut",
          value: "CT"
        },
        {
          text: "Delaware",
          value: "DE"
        },
        {
          text: "District Of Columbia",
          value: "DC"
        },
        {
          text: "Florida",
          value: "FL"
        },
        {
          text: "Georgia",
          value: "GA"
        },
        {
          text: "Hawaii",
          value: "HI"
        },
        {
          text: "Idaho",
          value: "ID"
        },
        {
          text: "Illinois",
          value: "IL"
        },
        {
          text: "Indiana",
          value: "IN"
        },
        {
          text: "Iowa",
          value: "IA"
        },
        {
          text: "Kansas",
          value: "KS"
        },
        {
          text: "Kentucky",
          value: "KY"
        },
        {
          text: "Louisiana",
          value: "LA"
        },
        {
          text: "Maine",
          value: "ME"
        },
        {
          text: "Maryland",
          value: "MD"
        },
        {
          text: "Massachusetts",
          value: "MA"
        },
        {
          text: "Michigan",
          value: "MI"
        },
        {
          text: "Minnesota",
          value: "MN"
        },
        {
          text: "Mississippi",
          value: "MS"
        },
        {
          text: "Missouri",
          value: "MO"
        },
        {
          text: "Montana",
          value: "MT"
        },
        {
          text: "Nebraska",
          value: "NE"
        },
        {
          text: "Nevada",
          value: "NV"
        },
        {
          text: "New Hampshire",
          value: "NH"
        },
        {
          text: "New Jersey",
          value: "NJ"
        },
        {
          text: "New Mexico",
          value: "NM"
        },
        {
          text: "New York",
          value: "NY"
        },
        {
          text: "North Carolina",
          value: "NC"
        },
        {
          text: "North Dakota",
          value: "ND"
        },
        {
          text: "Ohio",
          value: "OH"
        },
        {
          text: "Oklahoma",
          value: "OK"
        },
        {
          text: "Oregon",
          value: "OR"
        },
        {
          text: "Palau",
          value: "PW"
        },
        {
          text: "Pennsylvania",
          value: "PA"
        },
        {
          text: "Puerto Rico",
          value: "PR"
        },
        {
          text: "Rhode Island",
          value: "RI"
        },
        {
          text: "South Carolina",
          value: "SC"
        },
        {
          text: "South Dakota",
          value: "SD"
        },
        {
          text: "Tennessee",
          value: "TN"
        },
        {
          text: "Texas",
          value: "TX"
        },
        {
          text: "Utah",
          value: "UT"
        },
        {
          text: "Vermont",
          value: "VT"
        },
        {
          text: "Virgin Islands",
          value: "VI"
        },
        {
          text: "Virginia",
          value: "VA"
        },
        {
          text: "Washington",
          value: "WA"
        },
        {
          text: "West Virginia",
          value: "WV"
        },
        {
          text: "Wisconsin",
          value: "WI"
        },
        {
          text: "Wyoming",
          value: "WY"
        }
      ]
    }
  },
  methods: {
    filterTable(row, rowName){
      row[rowName] === 1
    },
    reset(){
      for(let key in this.searchMobile){
        if(Object.keys(this.searchMobile).includes(key)){
          if(typeof this.searchMobile[key] === 'boolean'){
            this.searchMobile[key] = false
          }else{
            this.searchMobile[key] = '';
          }
        }
      }
      this.filterOn = false;
      this.dataFiltered = [];
    },
    filterMobile(){
      this.dataFiltered = [...this.data];
      for(let key in this.searchMobile){
        if(Object.keys(this.searchMobile).includes(key)){
          this.dataFiltered = this.filterVal(this.dataFiltered, key)
        }
      }
      this.filterOn = true;
    },
    filterVal(arr, key){
      if(typeof this.searchMobile[key] === 'boolean'){
        if(this.searchMobile[key]){
          return arr.filter(x => x[key] === 1)
        }else{
          return arr
        }
      }else{
        if(this.searchMobile[key].length > 0){
          return arr.filter(x => x[key] === this.searchMobile[key])
        }else{
          return arr
        }
      }
    }
  }
}
</script>
<style scoped>
.vertical-align-middle{
  vertical-align: middle;
  height: 1em;
  display: inline-block;
}
</style>
