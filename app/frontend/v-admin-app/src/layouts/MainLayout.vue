<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          @click="toggleLeftDrawer"
          icon="menu"
          aria-label="Menu"
        />
        <q-toolbar-title>
          <strong>Property</strong><span style="color: black">Web</span
          ><strong class="navy--text text--darken-1">Builder</strong> &copy;
          2022 Admin
        </q-toolbar-title>
        <q-space />
        <div class="q-gutter-sm row items-center no-wrap">
          <q-btn
            round
            dense
            flat
            color="white"
            :icon="$q.fullscreen.isActive ? 'fullscreen_exit' : 'fullscreen'"
            @click="$q.fullscreen.toggle()"
            v-if="$q.screen.gt.sm"
          >
          </q-btn>
          <!-- <q-btn
            round
            dense
            flat
            color="white"
            icon="fab fa-github"
            type="a"
            href="/"
            target="_blank"
          >
          </q-btn>
          <q-btn
            round
            dense
            flat
            icon="fas fa-heart"
            style="color: #9d4182 !important"
            type="a"
            href="/"
            target="_blank"
          >
          </q-btn>
          <q-btn round dense flat color="white" icon="notifications">
            <q-badge color="red" text-color="white" floating> 5 </q-badge>
            <q-menu>
              <q-list style="min-width: 100px">
                <q-card class="text-center no-shadow no-border">
                  <q-btn
                    label="View All"
                    style="max-width: 120px !important"
                    flat
                    dense
                    class="text-indigo-8"
                  ></q-btn>
                </q-card>
              </q-list>
            </q-menu>
          </q-btn>
          <q-btn round flat>
            <q-avatar size="26px">
              <img src="https://cdn.quasar.dev/img/boy-avatar.png" />
            </q-avatar>
          </q-btn> -->
        </div>
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
      class="bg-primary text-white"
    >
      <q-list class="q-pt-xl q-mt-xl">
        <!-- <q-item to="/" active-class="q-item-no-link-highlighting">
          <q-item-section avatar>
            <q-icon name="dashboard" />
          </q-item-section>
          <q-item-section>
            <q-item-label>Dashboard</q-item-label>
          </q-item-section>
        </q-item> -->
        <q-item
          :exact="true"
          :to="{ name: 'rAgencyEditGeneral' }"
          active-class="q-item-no-link-highlighting"
        >
          <q-item-section avatar>
            <q-icon name="real_estate_agent" />
          </q-item-section>
          <q-item-section>
            <q-item-label>Agency</q-item-label>
          </q-item-section>
        </q-item>
        <q-item
          :exact="false"
          :to="{
            name: 'rTranslationsEditBatch',
            params: { tBatchId: 'extras' },
          }"
          active-class="q-item-no-link-highlighting"
        >
          <q-item-section avatar>
            <q-icon name="language" />
          </q-item-section>
          <q-item-section>
            <q-item-label>Translations</q-item-label>
          </q-item-section>
        </q-item>
        <!-- <q-item to="/Dashboard2" active-class="q-item-no-link-highlighting">
          <q-item-section avatar>
            <q-icon name="dashboard" />
          </q-item-section>
          <q-item-section>
            <q-item-label>CRM Dashboard</q-item-label>
          </q-item-section>
        </q-item> -->
        <q-expansion-item
          :default-opened="true"
          aria-expanded="true"
          icon="location_city"
          label="Properties"
        >
          <q-list class="q-pl-lg">
            <q-item
              :exact="true"
              :to="{ name: 'rPropertiesList' }"
              active-class="q-item-no-link-highlighting"
            >
              <q-item-section avatar>
                <q-icon name="list" />
              </q-item-section>
              <q-item-section>
                <q-item-label>List All</q-item-label>
              </q-item-section>
            </q-item>
          </q-list>
        </q-expansion-item>
        <q-expansion-item
          :default-opened="true"
          aria-expanded="true"
          icon="desktop_mac"
          label="Website"
        >
          <q-list class="q-pl-lg">
            <q-item
              :exact="false"
              :to="{ name: 'rWebsiteEditGeneral' }"
              active-class="q-item-no-link-highlighting"
            >
              <q-item-section avatar>
                <q-icon name="settings" />
              </q-item-section>
              <q-item-section>
                <q-item-label>Settings</q-item-label>
              </q-item-section>
            </q-item>
            <q-item
              :exact="false"
              :to="{ name: 'rWebsiteEditFooter' }"
              active-class="q-item-no-link-highlighting"
            >
              <q-item-section avatar>
                <q-icon name="lock" />
              </q-item-section>
              <q-item-section>
                <q-item-label>Footer</q-item-label>
              </q-item-section>
            </q-item>
            <!-- <q-item-label header class="text-weight-bolder text-white"
              >Generic</q-item-label
            >
            <q-item to="/" active-class="q-item-no-link-highlighting">
              <q-item-section avatar>
                <q-icon name="person" />
              </q-item-section>
              <q-item-section>
                <q-item-label>User Profile</q-item-label>
              </q-item-section>
            </q-item> -->
          </q-list>
        </q-expansion-item>
        <q-expansion-item
          :default-opened="true"
          aria-expanded="true"
          icon="pages"
          label="Pages"
        >
          <q-list class="q-pl-lg">
            <q-item
              :exact="false"
              :to="{
                name: 'rPagesEditTab',
                params: { pageName: 'home', pageTabName: 'title' },
              }"
              active-class="q-item-no-link-highlighting"
            >
              <q-item-section>
                <q-item-label>Home</q-item-label>
              </q-item-section>
            </q-item>
            <q-item
              v-for="pageToEdit in pagesToEdit"
              :key="pageToEdit"
              :exact="false"
              :to="{
                name: 'rPagesEditTab',
                params: { pageName: pageToEdit.pageName, pageTabName: 'title' },
              }"
              active-class="q-item-no-link-highlighting"
            >
              <q-item-section>
                <q-item-label>{{ pageToEdit.label }}</q-item-label>
              </q-item-section>
            </q-item>
          </q-list>
        </q-expansion-item>
      </q-list>
    </q-drawer>

    <q-page-container class="bg-grey-2">
      <router-view
        :currentWebsite="currentWebsite"
        :currentAgency="currentAgency"
      />
    </q-page-container>
  </q-layout>
</template>
<script>
import useAgency from "~/v-admin-app/src/compose/useAgency.js"
import useTranslations from "~/v-admin-app/src/compose/useTranslations.js"
import { defineComponent, ref } from "vue"
export default defineComponent({
  name: "MainLayout",
  inject: ["websiteProvider"],
  components: {
    // Messages
  },
  computed: {
    // supportedLocaleDetails() {
    //   let supportedLocales = this.currentWebsite.supported_locales || []
    //   let supportedLocaleDetails = []
    //   supportedLocales.forEach((localeWithVariant) => {
    //     let localeOnly = localeWithVariant.split("-")[0]
    //     supportedLocaleDetails.push({
    //       localeOnly: localeOnly,
    //       localeWithVariant: localeWithVariant,
    //       label: this.adminTranslations[localeOnly],
    //     })
    //   })
    //   return supportedLocaleDetails
    // },
  },
  mounted: function () {
    this.getAgency()
      .then((response) => {
        this.currentAgency = response.data.agency
        this.currentAgency.primaryAddress = response.data.primary_address
        this.currentWebsite = response.data.website
        this.websiteProvider.setCurrentWebsite(response.data.website)
      })
      .catch((error) => {})
    let adminLocale = "en"
    // will only support English for admin from now forward
    this.getAdminTranslations(adminLocale)
      .then((response) => {
        this.adminTranslations = response.data[adminLocale]
        this.websiteProvider.setAdminTranslations(response.data[adminLocale])
      })
      .catch((error) => {})
  },
  data() {
    return {
      adminTranslations: {},
      currentWebsite: {},
      currentAgency: {
        attributes: {},
      },
      activeTab: null,
    }
  },
  setup() {
    const leftDrawerOpen = ref(false)
    const { getAgency } = useAgency()
    const { getAdminTranslations } = useTranslations()
    return {
      getAgency,
      getAdminTranslations,
      leftDrawerOpen,
      toggleLeftDrawer() {
        leftDrawerOpen.value = !leftDrawerOpen.value
      },
      pagesToEdit: [
        {
          label: "Sell",
          pageName: "sell",
        },
        {
          label: "About Us",
          pageName: "about-us",
        },
        {
          label: "Contact Us",
          pageName: "contact-us",
        },
        {
          label: "Legal Notice",
          pageName: "legal",
        },
        {
          label: "Privacy Policy",
          pageName: "privacy",
        },
      ],
    }
  },
})
</script>
