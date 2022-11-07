<template>
<div>
	<MkPagination v-slot="{items}" ref="list" :pagination="pagination">
		<MkA v-for="item in items" :key="item.id" :to="`/clips/${item.id}`" class="clippreview">
			<b>{{ item.name }}</b>
			<div v-if="item.description" class="description">{{ item.description }}</div>
		</MkA>
	</MkPagination>
</div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import MkPagination from '@/components/ui/pagination.vue';

export default defineComponent({
	components: {
		MkPagination,
	},

	props: {
		user: {
			type: Object,
			required: true
		},
	},

	data() {
		return {
			pagination: {
				endpoint: 'users/clips' as const,
				limit: 20,
				params: {
					userId: this.user.id,
				}
			},
		};
	},

	watch: {
		user() {
			this.$refs.list.reload();
		}
	},
});
</script>

<style lang="scss" scoped>
.clippreview {
    display: block;
    padding: 20px;
    margin: var(--margin) 0;
    background: var(--panel);
    border-radius: var(--radius);
    overflow: clip;
}
</style>
