<template>
  <div>
    <b-navbar toggleable="lg" type="dark" variant="info">
      <b-navbar-brand href="#">NavBar</b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav>
          <b-nav-item href="#">Link</b-nav-item>
          <b-nav-item href="#" disabled>Disabled</b-nav-item>
        </b-navbar-nav>

        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto">
          <b-nav-form>
            <b-form-input size="sm" class="mr-sm-2" placeholder="Search"></b-form-input>
            <b-button size="sm" class="my-2 my-sm-0" type="submit">Search</b-button>
          </b-nav-form>

          <b-nav-item-dropdown text="Lang" right>
            <b-dropdown-item href="#">EN</b-dropdown-item>
            <b-dropdown-item href=""><b-nav-text style="color: black" @click.stop>ES</b-nav-text></b-dropdown-item>
            <b-dropdown-item-text v-for="(menuInside, index) in formats" :key="`formatter-${index}`"
              ><div
                @click.stop
                style="
                  display: block;
                  width: 100%;
                  padding: 0.25rem 1.5rem;
                  clear: both;
                  font-weight: 400;
                  color: #212529;
                  text-align: inherit;
                  white-space: nowrap;
                  background-color: transparent;
                  border: 0;
                "
                v-if="menuInside.format.length === 0"
              >
                <b-button variant="outline-success" style="width: 100%" @click.self="show_alrt(index)">{{
                  menuInside.title
                }}</b-button>
              </div>
              <b-dd-group :header="menuInside.title" v-else>
                <b-dd-divider />
                <!-- :style="`width: ${100 / format.length}%`" -->
                <b-dropdown-item-button
                  v-for="(el, idx) in menuInside.format"
                  :key="`format-button-${idx}`"
                  variant="outline-success"
                  @click="cncl(index)"
                  >{{ el }}</b-dropdown-item-button
                >
                <b-dd-divider />
              </b-dd-group>
            </b-dropdown-item-text>
            <b-dropdown-item href="#">FA</b-dropdown-item>
          </b-nav-item-dropdown>

          <b-nav-item-dropdown right>
            <!-- Using 'button-content' slot -->
            <template #button-content>
              <em>User</em>
            </template>
            <b-dropdown-item href="#">Profile</b-dropdown-item>
            <b-dropdown-item href="#">Sign Out</b-dropdown-item>
          </b-nav-item-dropdown>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      formats: [
        { title: 'Спецификация', format: [] },
        { title: 'Техническое чего-то', format: [] }
      ]
    }
  },
  mounted() {
    this.$root.$on('bv::dropdown::hide', () => {
      this.formats = [
        { title: 'Спецификация', format: [] },
        { title: 'Техническое чего-то', format: [] }
      ]
    })
  },
  methods: {
    show_alrt(index) {
      this.formats = [
        { title: 'Спецификация', format: [] },
        { title: 'Техническое чего-то', format: [] }
      ]
      this.formats[index].format = ['xslx', 'pdf', 'docx', 'odt']
    },
    cncl(index) {
      this.formats[index].format = []
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.links {
  background-color: yellow;
}
</style>
