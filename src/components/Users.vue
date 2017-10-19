<template>
  <b-row class="users">
    <b-col cols="12">
      <b-row class="top-section">
        <b-col lg="6" sm="12">
          <h2>Users (stored in localStorage)<span v-if="len_users > 0">. We already have users</span></h2>
          <h3>Total de users: {{len_users}}</h3>
          <div class="form-container" v-on:keyup.13="add_user">
            <div class="form-group">
              <label for="name">Name</label>
              <b-form-input ref="name_input" class="form-control" v-model="new_user.name" id="name" placeholder="Enter name"></b-form-input>
            </div>
            <div class="form-group">
              <label for="phone">Phone</label>
              <b-form-input class="form-control" v-model="new_user.phone" id="phone" placeholder="Enter phone"></b-form-input>
            </div>
          </div>
          <div class="md-flex-100">
            <small>{{log}}</small>
          </div>
        </b-col>
      </b-row>
      <b-row>
        <b-col lg="3" md="6" class="text-center card_container" v-for="(user, idx) in users" :key="idx">
          <div class="card" style="width: 100%;">
            <div class="card-image" style="background-image: url(https://images.pexels.com/photos/285171/pexels-photo-285171.jpeg?h=180)"></div>
            <div class="card-block">
              <h4 class="card-title">{{user.name}}</h4>
              <p class="card-text description">{{user.phone}}</p>
              <div class="actions">
                <b-button variant="danger" v-on:click="open_modal(user)"><span class="fa fa-times"></span> <span>Delete User</span></b-button>
              </div>
            </div>
          </div>
        </b-col>
      </b-row>
    </b-col>
    <modal v-if="showModal" v-on:close="showModal = false">
      <h3 slot="header">Delete {{modal_item.name}}?</h3>
      <p slot="body">Phone: {{modal_item.phone}}</p>
      <div slot="footer" class="align-right">
        <b-button variant="danger" v-on:click="delete_user(modal_item)">
          Yes
        </b-button>
        <b-button variant="default" v-on:click="showModal = false">
          Cancel
        </b-button>
      </div>
    </modal>
  </b-row>
</template>
<script>
  export default {
    props: ['users'],
    data () {
      return {
        showModal: false,
        log: '',
        new_user: {name: '', phone: ''},
      }
    },
    methods: {
      add_user: function() {
        if(this.new_user.name.trim() == '' || this.new_user.phone.trim() == '') {
          alert('fill in all data correcly');
          return;
        }
        this.users.push(this.new_user);
        localStorage.setItem("users", JSON.stringify(this.users));
        this.new_user = {name: '',  phone: ''};
        this.$refs.name_input.$el.focus();
      },
      delete_user: function(user) {
        this.users.splice(this.users.findIndex((u, idx) => u == user), 1);
        localStorage.setItem("users", JSON.stringify(this.users));
        this.showModal = false;
      },
      open_modal: function(item) {
        this.modal_item = item;
        this.showModal = true;
      },
    },
    watch: {
      len_users: function(new_val, old_val) {
        this.log = 'We have ' +new_val+ ' users now, not ' +old_val+ ' anymore';
      }
    },
    computed: {
      len_users: function() {
        return this.users.length;
      }
    },
    mounted: function() {
      this.$refs.name_input.$el.focus();
    }
  }
</script>

<style scoped>
.actions span {
  color: #ffffff;
}
.top-section {
  padding: 15px 0;
}

</style>