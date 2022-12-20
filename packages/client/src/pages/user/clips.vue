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

<script lang="ts" setup>
import { computed } from 'vue';
import * as misskey from 'misskey-js';
import MkPagination from '@/components/MkPagination.vue';

const props = defineProps<{
	user: misskey.entities.User;
}>();

const pagination = {
	endpoint: 'users/clips' as const,
	limit: 20,
	params: computed(() => ({
		userId: props.user.id,
	})),
};
</script>

<style lang="scss" scoped>
.clippreview {
    display: block;
    padding: 20px;
    margin: 15px 26px;
    background: var(--panel);
    border-radius: var(--radius);
    overflow: clip;
}
</style>
