<template>
	<div class="flex flex-col w-full">
		<div class="flex border-b h-[52px] px-[24px] shrink-0">
			<div class="grow my-auto text-[16px] font-semibold text-gray-900">
				Tickets
			</div>
		</div>
		<div class="w-full max-w-full grow-0">
			<ListManager
				ref="miniTicketList"
				:options="{
					doctype: 'Ticket',
					fields: [
						'subject',
						'ticket_type',
						'status',
						'_seen'
					],
					limit: 50,
					order_by: 'modified desc',
					filters: {
						'contact': ['=', contact]
					},
					route_query_pagination: true
				}"
			>
				<template #body="{ manager }">
					<div >
						<MiniTicketList 
							:manager="manager" 
							size="lg"
							class="overflow-y-scroll"
							:style="{ height: viewportWidth > 768 ? 'calc(100vh - 144px)' : null }"
						/>
						<ListPageController :manager="manager" />
					</div>
				</template>
			</ListManager>
		</div>
	</div>
</template>

<script>
import MiniTicketList from '@/components/desk/global/MiniTicketList.vue'
import ListManager from '@/components/global/ListManager.vue'
import ListPageController from '@/components/global/ListPageController.vue'
import { inject } from 'vue'

export default {
	name: 'ContactRelatedInfo',
	props: ['contact'],
	components: {
		MiniTicketList,
		ListManager,
		ListPageController
	},
	setup() {
		const viewportWidth = inject('viewportWidth')

		return {
			viewportWidth
		}
	},
}
</script>

<style>

</style>