<template>
  <div class="servers-view">
    <b-table
      :items="servers"
      :fields="fields"
      sort-by="state"
      striped
    >
      <template #cell(state)="{ item: { server } }">
        <smoo-server-state :server="server" @state="server.state = $event"/>
      </template>

      <template #head(server)>
        Server
        <sup id="servers-hostname" @click.stop.prevent><b-icon icon="info-circle-fill"/></sup>
        <b-tooltip target="servers-hostname" triggers="hover" style="text-align: justified;">
          The <code>Host</code> entry is a convenient alternative to the IPv4 address.
          But this <a-ext href="https://github.com/CraftyBoss/SuperMarioOdysseyOnline/pull/20">feature</a-ext>
          isn't part of the latest mod release yet.
        </b-tooltip>
      </template>

      <template #cell(server)="{ item: { server: { host, ip } } }">
        <span class="host" v-if="host">{{ host }}</span>
        <br v-if="host && ip"/>
        <span class="ip" v-if="ip">{{ ip }}</span>
      </template>

      <template #cell(port)="{ item: { server: { port } } }">
        <span>{{ port || defaultPort }}</span>
      </template>

      <template #cell(location)="{ item }">
        <div>
          <span class="flag-icon">
            <country-flag
              :title="item.location.name"
              :country="item.location.flag"
              size="normal"
              rounded
            />
          </span>
          <span class="name"> {{ item.location.name }}</span>
        </div>
      </template>

      <template #cell(version)="{ item: { version } }">
        <span v-html="version"/>
      </template>

    </b-table>
  </div>
</template>

<style lang="scss" src="./servers.scss"/>

<script lang="ts" src="./servers.ts"/>
