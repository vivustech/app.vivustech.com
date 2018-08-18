<template>
  <div>
  
  <!-- Right Drawer -->
    <v-navigation-drawer
      v-model="drawerRight"
      enable-resize-watcher
      fixed
      right
      clipped
      app
    >
      <v-toolbar flat class="transparent" color="blue darken-2">
        <v-list class="pa-0">
          <v-list-tile avatar>
            <v-list-tile-avatar>
              <img src="https://randomuser.me/api/portraits/men/85.jpg">
            </v-list-tile-avatar>

            <v-list-tile-content>
              <v-list-tile-title>{{ dbData.userName }}</v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>
        </v-list>
      </v-toolbar>

      <v-list class="pt-0" dense>
        <v-divider></v-divider>

        <v-list-tile
          v-for="item in items"
          :key="item.title"
        >
          <v-list-tile-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-tile-action>

          <v-list-tile-content>
            <v-list-tile-title>{{ item.title }}</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer>
  
  <!-- Top toolbar -->
    <v-toolbar
      fixed
      app
      clipped-right
    >
      <v-toolbar-side-icon @click.stop="drawer = !drawer"></v-toolbar-side-icon>
      <v-toolbar-title>{{ pageName }}</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-toolbar-side-icon @click.stop="drawerRight = !drawerRight"></v-toolbar-side-icon>
    
  
  </v-toolbar>
      
  <!-- Left Drawer -->
  <v-navigation-drawer
  v-model="drawer"
    stateless
    value="true"
  fixed
  class="blue-grey darken-4"
  dark
  app
  >
      <v-list class="blue-grey darken-4" dark>
      
        <v-list-tile>
    <v-list-tile-title center><h3 class="text-xs-center" style="letter-spacing: 4px;">{{ dbData.companyName }}</h3></v-list-tile-title>
    
      </v-list-tile>
        
      <!-- Home tile -->
      <v-list-tile>
        <v-list-tile-action>
          <v-icon>home</v-icon>
        </v-list-tile-action>
    <v-list-tile-title>Home</v-list-tile-title>
    
      </v-list-tile>

    <!-- User group -->
      <v-list-group
        prepend-icon="account_circle"
      >
        <v-list-tile slot="activator">
          <v-list-tile-title>Users</v-list-tile-title>
        </v-list-tile>

        <v-list-group
          no-action
          sub-group
          value="true"
        >
          <v-list-tile slot="activator">
      
            <v-list-tile-title>Admin</v-list-tile-title>
      
          </v-list-tile>

          <v-list-tile
            v-for="(admin, i) in admins"
            :key="i"
          >
            <v-list-tile-title v-text="admin[0]"></v-list-tile-title>
            <v-list-tile-action>
              <v-icon v-text="admin[1]"></v-icon>
            </v-list-tile-action>
          </v-list-tile>
        </v-list-group>

        <v-list-group
          sub-group
          no-action
        >
          <v-list-tile slot="activator">
            <v-list-tile-title>Actions</v-list-tile-title>
          </v-list-tile>

          <v-list-tile
            v-for="(crud, i) in cruds"
            :key="i"
          >
            <v-list-tile-title v-text="crud[0]"></v-list-tile-title>
            <v-list-tile-action>
              <v-icon v-text="crud[1]"></v-icon>
            </v-list-tile-action>
          </v-list-tile>
        </v-list-group>
      </v-list-group>
    
    
    <!-- New group -->
    <v-list-group
        prepend-icon="apps"
        value="true"
      >
        <v-list-tile slot="activator">
          <v-list-tile-title>Apps</v-list-tile-title>
        </v-list-tile>

      <v-list-tile
            v-for="(app, i) in apps"
            :key="i"
          >
            <v-list-tile-title v-text="app[0]"></v-list-tile-title>
            <v-list-tile-action>
              <v-icon v-text="app[1]"></v-icon>
            </v-list-tile-action>
          </v-list-tile>
  </v-list-group>  
    </v-list>
  </v-navigation-drawer>  
      
  <!-- Main Content -->
    <v-content style="background-color: #dedede">
      <v-container grid-list-xl fluid><v-layout wrap >
          
          
          <!-- PROJECT CARD -->
          <v-flex xs12>
            <v-card style="min-width:300px;max-width:800px;margin:0 auto; padding:20px;">
              <v-card-title primary-title>
                <div class="headline" style="margin:0 auto;">Summer 2018 Project</div>              
              </v-card-title>
              
              <v-card-text class="pa-0">
                <v-container class="pa-0">
                  
                  <div class="text-xs-center" >
                    <div class="text-xs-center">
                      <v-btn
                        color="primary"
                        dark
                        @click="resetChips"
                      >
                        Reset Chips
                      </v-btn>
                    </div>
                    <v-chip v-for="(chip, i) in chips"
                      :key="i"
                            v-if="chip.show"
                      close text-color="white"
                      :color="chip.color"
                      @input="removeChip(chip)"
                    ><v-avatar>
                            <img src="https://randomuser.me/api/portraits/men/35.jpg" alt="trevor">
                          </v-avatar>{{ chip.name }}</v-chip>
                        
                      </div>
                  
          </v-container>
                </v-card-text>
            </v-card>
          </v-flex>
          </v-layout>
                
          
          <!-- SIGN UP BOX -->
          <v-flex xs12>
            <v-card style="min-width:300px;max-width:800px;margin:0 auto; padding:20px;">
              <v-card-title primary-title>
                <div class="headline" style="margin:0 auto;">Sign Up</div>              
              </v-card-title>
              <v-card-text>
                <v-form ref="form" v-model="valid" lazy-validation>
                <v-text-field
                  v-model="name"
                  :rules="nameRules"
                  :counter="10"
                  label="Name"
                  required
                ></v-text-field>
                <v-text-field
                  v-model="email"
                  :rules="emailRules"
                  label="E-mail"
                  required
                ></v-text-field>
                <v-select
                  v-model="select"
                  :items="items"
                  :rules="[v => !!v || 'Item is required']"
                  label="Item"
                  required
                ></v-select>
                <v-checkbox
                  v-model="checkbox"
                  :rules="[v => !!v || 'You must agree to continue!']"
                  label="Do you agree?"
                  required
                ></v-checkbox>

                <v-btn
                  :disabled="!valid"
                  @click="submit"
                >
                  submit
                </v-btn>
                <v-btn @click="clear">clear</v-btn>
              </v-form>
                </v-card-text>
            </v-card>
          </v-flex>
          
          
          <!-- TEXT BOXES -->
      <v-flex v-for="i in 10"  :key="i">
            <v-card color="white" class="black--text" style="height:200px;min-width:300px;max-width:1400px;margin: 10px auto;">
              <v-card-title primary-title>
                <div class="headline">Unlimited music now</div>
				
              </v-card-title>
			  <v-card-text>
			  <div style="word-wrap: break-word;min-width:150px;"> asdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasdfasd
			  </div>
			  </v-card-text>
              <v-card-actions>
                <v-btn flat dark>Listen now</v-btn>
              </v-card-actions>
            </v-card>
          </v-flex>
      </v-container>
    </v-content>
  
  <!-- Footer -->
    <v-footer dark class="whitef--text" app>
      <span>Vuetify</span>
      <v-spacer></v-spacer>
      <span>&copy; 2018</span>
    </v-footer>
    </div>
</template>


<script>

export default {
  data () {
    return {
      admins: [
        ['Management', 'people_outline'],
        ['Settings', 'settings']
      ],
      cruds: [
        ['Create', 'add'],
        ['Read', 'insert_drive_file'],
        ['Update', 'update'],
        ['Delete', 'delete']
      ],
      items: [
        { title: 'Home', icon: 'dashboard' },
        { title: 'About', icon: 'question_answer' }
      ],
      apps: [
        ['Test', 'language']
      ],
      dbData: {
        companyName: 'TEST COMPANY',
        userName: 'John Wick'
      },
      pageName: 'Home',
      drawer: false,
      drawerRight: false,
      right: null,
      left: null,
      assignedUsers: [
        { name: 'Tanner Grant', color: 'primary', show: true },
        { name: 'John Goodart', color: 'warning', show: true }
      ],
      chips: [
        {name: 'Tanner Grant', show: true, color: 'blue'},
        {name: 'John Goodart', show: true, color: 'green'},
        {name: 'Angela Grant', show: true, color: 'red'},
        {name: 'Chris Burgess', show: true, color: 'purple'}
      ],
      checkbox: true,
      valid: true,
      select: true,
      emailRules: ['These are the email rules..', 'sadf'],
      email: 'test@test.com',
      nameRules: ['These are the name rules..', 'asdf'],
      name: 'John Wick'
    }
  },
  props: {
    source: String
  },
  methods: {
    removeChip (chip) {
      chip.show = false
    },
    resetChips () {
      for (var i in this.chips) {
        this.chips[i].show = true
      }
    },
    submit () {
      console.log('Submit data')
    },
    clear () {
      console.log('Clear form')
    }
  }
}
</script>

<style scoped>
.assigned-wrapper {
  background-color: lightgrey;
  margin: 0 auto;
  padding: 5px;
}

.assigned-title {
  background-color: lightblue;
  padding: 5px;
}

.assigned-list {
  padding: 5px;
}
</style>