<template>
  <div>
    <md-layout md-gutter>
      <md-layout md-flex-small="50" md-flex-xlarge="25">
        <span class="counter">
          <span class="counter-up" :data-total="dashboard.TasksCreatedCount">0</span>
          <br>
          <span style="font-size: small; opacity: 0.75;">Created</span>
        </span>
      </md-layout>
      <md-layout md-flex-small="50" md-flex-xlarge="25">
        <span class="counter">
          <span class="counter-up" :data-total="dashboard.TasksAssignedCount">0</span>
          <br>
          <span style="font-size: small; opacity: 0.75;">Assigned</span>
        </span>
      </md-layout>
      <md-layout md-flex-small="50" md-flex-xlarge="25">
        <span class="counter">
          <span class="counter-up" :data-total="dashboard.TasksCompletedCount">0</span>
          <br>
          <span style="font-size: small; opacity: 0.75;">Completed</span>
        </span>
      </md-layout>
      <md-layout md-flex-small="50" md-flex-xlarge="25">
        <span class="counter">
          <span class="counter-up" :data-total="dashboard.LogsCount">0</span>
          <br>
          <span style="font-size: small; opacity: 0.75;">Comments</span>
        </span>
      </md-layout>
    </md-layout>
    <br>
    <md-layout md-gutter="40">
      <md-layout md-gutter="8" md-flex-xsmall="100" md-flex-small="70" md-flex-medium="66" md-flex-large="80" md-flex-xlarge="80">
        <md-layout>
          chart
        </md-layout>
        <md-layout>
          chart
        </md-layout>
        <md-layout>
          chart
        </md-layout>
      </md-layout>
      <md-layout md-flex-xsmall="100" md-flex-small="30" md-flex-medium="33" md-flex-large="20" md-flex-xlarge="20">
        <md-list class="full-width">
          <md-subheader class="md-inset">My Tasks</md-subheader>
          <md-list-item>
            <md-icon>add</md-icon>
            <span>
              <router-link to="/tasks/create">New</router-link>
            </span>
          </md-list-item>
          <md-list-item>
            <md-icon>assignment_return</md-icon>
            <span>
              <router-link :to="{path: '/tasks', query: {sub: 'Assigned'}}">Assigned to me
                <md-chip>{{dashboard.TasksAssignedCount}}</md-chip>
              </router-link>
            </span>
          </md-list-item>
          <md-list-item>
            <md-icon>assignment</md-icon>
            <span>
              <router-link :to="{path: '/tasks', query: {sub: 'Created'}}">Created by me
                <md-chip>{{dashboard.TasksCreatedCount}}</md-chip>
              </router-link>
            </span>
          </md-list-item>
          <md-list-item>
            <md-icon>assignment_turned_in</md-icon>
            <span>
              <router-link :to="{path: '/tasks', query: {sub: 'Completed'}}">Completed
                <md-chip>{{dashboard.TasksCompletedCount}}</md-chip>
              </router-link>
            </span>
          </md-list-item>
          <md-list-item>
            <md-icon>delete</md-icon>
            <span>
              <router-link to="/tasks/trash">Trash
                <md-chip>{{dashboard.TasksDeletedCount}}</md-chip>
              </router-link>
            </span>
          </md-list-item>
          <md-subheader class="md-inset">Messages</md-subheader>
          <md-list-item>
            <md-icon>add</md-icon>
            <span>
              <router-link :to="{path: '/messages', query: {folder: 'compose'}}">New</router-link>
            </span>
          </md-list-item>
          <md-list-item>
            <md-icon>mail</md-icon>
            <span>
              <router-link :to="{path: '/messages', query: {folder: 'inbox'}}">Inbox
                <md-chip>{{dashboard.MessagesReceivedCount}}</md-chip>
              </router-link>
            </span>
          </md-list-item>
          <md-list-item>
            <md-icon>send</md-icon>
            <span>
              <router-link :to="{path: '/messages', query: {folder: 'sent'}}">Sent
                <md-chip>{{dashboard.MessagesSentCount}}</md-chip>
              </router-link>
            </span>
          </md-list-item>
          <md-list-item>
            <md-icon>delete</md-icon>
            <span>
              <router-link :to="{path: '/messages', query: {folder: 'trash'}}">Trash
                <md-chip>{{dashboard.MessagesDeletedCount}}</md-chip>
              </router-link>
            </span>
          </md-list-item>
        </md-list>
      </md-layout>
    </md-layout>
  </div>
</template>
<script>
  import dashboard from 'services/dashboard'

  export default {
    data () {
      return {
        dashboard: {}
      }
    },
    components: {},
    created () {
      dashboard.get().then(res => {
        this.dashboard = res.data
      }).catch(err => {

      })
    }
  }

</script>
<style scoped>
  .counter {
    width: 50%;
    margin: 5px auto;
    text-align: center;
    padding: 10% 5%;
    font-size: 50px;
    background-color: #3f51b5;
    color: #fff;
    text-shadow: 0 0 3px black;
    border-radius: 3px;
  }

  a .md-chip {
    float: right;
  }

  .chart-full-width {
    width: 100%;
  }

  .chart-full-width canvas {
    width: 100%;
  }
</style>
