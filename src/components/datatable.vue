<template>
  <section>
    <b-table
        :data="data"
        paginated
        striped
        :per-page="isMobile() ? 3 : 8"
        aria-next-label="Next page"
        aria-previous-label="Previous page"
        aria-page-label="Page"
        aria-current-label="Current page">
      <b-table-column field="PSAP_Name" label="PSAP Name" searchable sortable v-slot="props">
        {{ props.row.PSAP_Name }}
      </b-table-column>
      <b-table-column field="County" label="County" searchable sortable v-slot="props">
        {{ props.row.County }}
      </b-table-column>
      <b-table-column field="City" label="City" searchable sortable v-slot="props">
        {{ props.row.City }}
      </b-table-column>
      <b-table-column field="State" label="State" width="3em" searchable sortable v-slot="props">
        {{ props.row.State }}
      </b-table-column>
      <b-table-column field="Zip" label="ZIP" numeric searchable sortable v-slot="props">
        {{ props.row.Zip }}
      </b-table-column>
      <b-table-column field="TTY" label="Text"  searchable :custom-search="filterTable('TTY')" >
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
  created(){
    this.isMobile();
  },
  data() {
    return {
      name: 'datatable',
      data: data
    }
  },
  methods: {
    isMobile() {
      return screen.width <= 760;
    },
    filterTable(row, rowName){
      return row[rowName] === 1
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
