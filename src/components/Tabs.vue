<template>
	<div class="tab-container">
	  <div class="tabs">
	    <ul>
	      <li class="transitional" v-for="tab in tabs" :class="{ 'is-active': tab.isActive }">
	        <a :href="tab.href" @click="selectTab(tab)">{{ tab.name }}</a>
	      </li>
	    </ul>
	  </div>

	  <div class="tabs-details">
	    <slot></slot>
	  </div>
	</div>
</template>

<script>
import Tab from './Tab.vue';

export default {
	name: 'tabs',
	data() {
	  return { tabs: [] }
	},
	created() {
	  this.tabs = this.$children;
	},
	methods: {
	  selectTab: function(selectedTab) {
	    this.tabs.forEach(tab => {
	      tab.isActive = (tab.name == selectedTab.name);
	    });
	  }
	},
	components: {
	  Tab
	},
}
</script>

<style lang="scss">
@import '../assets/styles/_global.scss';

	.tabs {
		font-family: $serif;
		font-weight: 600;
		font-size: 30px;

		ul {
			list-style-type: none;
			margin: 0;
			padding: 0;

			li {
				display: inline-block;
				min-width: 45%;
				position: relative;

				@media (min-width: $tablet-portrait) {
					display: block;
					min-width: auto;
				}
			}

			li:not(:last-of-type) {
				margin-bottom: $gutter / 2;
				margin-right: $gutter;
			}

			a {
				color: $black;
				display: block;
				text-decoration: none;
				padding: 12px 20px;
			}
		} // ul
	} // .tabs

	.tabs-details {

		@media (min-width: $tablet-portrait) {
			margin-right: $gutter * 2;
			width: 60%;
		}
	}
</style>
