<script setup lang="ts">
import Query from '@/models/Query.ts'
import QueryBuilder from './components/QueryBuilder.vue'
import { ref } from 'vue'

const filter = ref({
  logicalOperator: 'AND',
  children: [
    {
      type: 'query-builder-group',
      query: {
        logicalOperator: 'OR',
        children: [
          {
            type: 'query-builder-rule',
            query: {
              rule: 'ambient',
              operator: 'IN',
              operand: 'ambient',
              value: [ /* your values here */ ]
            },
            originalIndex: 0
          },
          {
            type: 'query-builder-rule',
            query: {
              rule: 'cocain',
              operator: 'IN',
              operand: 'cocain',
              value: [ /* your values here */ ]
            },
            originalIndex: 1
          },
          {
            type: 'query-builder-group',
            query: {
              logicalOperator: 'AND',
              children: [
                {
                  type: 'query-builder-rule',
                  query: {
                    rule: '',
                    operator: 'eq',
                    operand: 'customerID',
                    value: '12400'
                  },
                  originalIndex: 0
                }
              ]
            },
            originalIndex: 2
          }
        ]
      }
    },
    {
      type: 'query-builder-rule',
      query: {
        rule: 'statusbar',
        operator: 'IN',
        operand: 'statusbar',
        value: [ /* your values here */ ]
      }
    }
  ]
} as Query)

const emptyQuery = ref({} as Query)

// Custom fields and operators
const filterFields = ref<Array<string>>([
  'id', 'name', 'date', 'type', 'customerID', 'statusbar', 'cocain', 'ambient'
])
import { Operator } from '@/types.ts';
const filterOperators = ref<Operator[]>([
  { value: 'eq', text: '=', type: 'string' },
  { value: 'ne', text: '!=', type: 'string' },
  { value: 'gt', text: '>', type: 'string' },
  { value: 'not in', text: 'not in', type: 'array' }
]);

</script>

<template>
  <v-app>
    <v-app-bar>
      <v-app-bar-nav-icon>
        <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="50" height="50" />
      </v-app-bar-nav-icon>
      <v-app-bar-title>Vue.js 3 query builder</v-app-bar-title>
    </v-app-bar>
    <v-main style="width: 100%">
      <v-container :fluid="true">
        <h1>Examples:</h1>
        <hr />
        <div>
          <h2>Existing query object:</h2>
          <query-builder
            v-model="filter"
            :filter-fields="filterFields"
            :filter-operators="filterOperators"
          ></query-builder>
        </div>
        <hr />
        <div>
          <h2>Empty object {}:</h2>
          <query-builder
            v-model="emptyQuery"
            :filter-fields="filterFields"
            :filter-operators="filterOperators"
          ></query-builder>
        </div>
      </v-container>
    </v-main>
  </v-app>
</template>

<style scoped></style>
