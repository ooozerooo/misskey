<template>
<MkStickyContainer>
	<template #header><MkPageHeader :actions="headerActions" :tabs="headerTabs"/></template>
	<MkSpacer :content-max="800">
		<MkPagination v-slot="{items}" :pagination="pagination" class="ruryvtyk _gaps_m">
			<section v-for="(announcement, i) in items" :key="announcement.id" class="announcement _panel">
				<div class="header"><span v-if="$i && !announcement.isRead">đ </span>{{ announcement.title }}</div>
				<div class="content">
					<Mfm :text="announcement.text"/>
					<img v-if="announcement.imageUrl" :src="announcement.imageUrl"/>
				</div>
				<div v-if="$i && !announcement.isRead" class="footer">
					<MkButton primary @click="read(items, announcement, i)"><i class="ti ti-check"></i> {{ $ts.gotIt }}</MkButton>
				</div>
			</section>
		</MkPagination>
	</MkSpacer>
</MkStickyContainer>
</template>

<script lang="ts" setup>
import { } from 'vue';
import MkPagination from '@/components/MkPagination.vue';
import MkButton from '@/components/MkButton.vue';
import * as os from '@/os';
import { i18n } from '@/i18n';
import { definePageMetadata } from '@/scripts/page-metadata';

const pagination = {
	endpoint: 'announcements' as const,
	limit: 10,
};

// TODO: ăăăŻćźèłȘçă«èŠȘăłăłăăŒăăłăăăć­ăłăłăăŒăăłăăźăă­ăăăŁăć€æŽăăŠăăźă§ăȘăăšăăăă
function read(items, announcement, i) {
	items[i] = {
		...announcement,
		isRead: true,
	};
	os.api('i/read-announcement', { announcementId: announcement.id });
}

const headerActions = $computed(() => []);

const headerTabs = $computed(() => []);

definePageMetadata({
	title: i18n.ts.announcements,
	icon: 'ti ti-speakerphone',
});
</script>

<style lang="scss" scoped>
.ruryvtyk {
	> .announcement {
		padding: 16px;

		> .header {
			margin-bottom: 16px;
			font-weight: bold;
		}

		> .content {
			> img {
				display: block;
				max-height: 300px;
				max-width: 100%;
			}
		}

		> .footer {
			margin-top: 16px;
		}
	}
}
</style>
