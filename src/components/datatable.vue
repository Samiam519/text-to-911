<template>
  <section>
    <b-table
        :data="data"
        sticky-header
        paginated
        striped
        :loading="data.length < 1"
        per-page="25"
        height="45em"
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
      <b-table-column field="TTY" label="TEXT" v-slot="props">
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
      </b-table-column>
      <b-table-column field="Web_Browser" label="Web Browser" v-slot="props">
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
      </b-table-column>
      <b-table-column field="DirectIP" label="Direct IP" v-slot="props">
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
      </b-table-column>
      <b-table-column field="RTT" label="RTT" v-slot="props">
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
    </b-table>
  </section>
</template>

<script>
const data = require( '../assets/text_911_master_psap_registry.json');

export default {
  data() {
    return {
      name: 'datatable',
      data: data,
      columns: [
        {
          field: 'PSAP ID',
          label: 'PSAP ID',
          numeric: true,
          sortable: true
        },
        {
          field: 'PSAP Name',
          label: 'PSAP Name',
          searchable: true,
          sortable: true
        },
        {
          field: 'County',
          label: 'County',
          searchable: true,
          sortable: true
        },
        {
          field: 'City',
          label: 'City',
          searchable: true,
          sortable: true
        },
        {
          field: 'State',
          label: 'State',
          searchable: true,
          sortable: true
        },
        {
          field: 'Zip',
          label: 'ZIP',
          searchable: true,
          numeric: true,
          sortable: true
        },
        {
          field: 'Text to TTY',
          label: 'Text',
          sortable: true
        },
        {
          field: 'Web Browser',
          label: 'Web Browser',
          sortable: true
        },
        {
          field: 'DirectIP',
          label: 'Direct IP',
          sortable: true
        },
        {
          field: 'RTT',
          label: 'RTT',
          sortable: true
        },
        {
          field: 'Other',
          label: 'Other',
          sortable: true
        }
      ]
    }
  }
}
</script>
