<!--
  - @copyright Copyright (c) 2020 Georg Ehrke <oc.list@georgehrke.com>
  - @author Georg Ehrke <oc.list@georgehrke.com>
  -
  - @license GNU AGPL version 3 or any later version
  -
  - This program is free software: you can redistribute it and/or modify
  - it under the terms of the GNU Affero General Public License as
  - published by the Free Software Foundation, either version 3 of the
  - License, or (at your option) any later version.
  -
  - This program is distributed in the hope that it will be useful,
  - but WITHOUT ANY WARRANTY; without even the implied warranty of
  - MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
  - GNU Affero General Public License for more details.
  -
  - You should have received a copy of the GNU Affero General Public License
  - along with this program. If not, see <http://www.gnu.org/licenses/>.
  -
  -->
<template>
	<Modal
		class="shortcut-overview-modal"
		size="normal"
		:title="$t('calendar', 'Shortcut overview')"
		@close="$emit('close')">
		<section
			v-for="category in shortcuts"
			:key="category.categoryId"
			class="shortcut-section">
			<h3 class="shortcut-section__header">
				{{ category.categoryLabel }}
			</h3>
			<div
				v-for="(shortcut, index) in category.shortcuts"
				:key="`${category.categoryId}-${index}`"
				class="shortcut-section-item">
				<span class="shortcut-section-item__keys">
					<template
						v-for="(keyCombination, index2) of shortcut.keys"
						class="shortcut-section-item__key-combination">
						<template v-for="(key, index3) in keyCombination">
							<kbd :key="`${category.categoryId}-${index}-${index2}-${index3}`">{{ key }}</kbd>
							<span
								v-if="index3 !== (keyCombination.length - 1)"
								:key="`${category.categoryId}-${index}-${index2}-${index3}`"
								class="shortcut-section-item__spacer">
								+
							</span>
						</template>
						<span
							v-if="index2 !== (shortcut.keys.length - 1)"
							:key="`${category.categoryId}-${index}-${index2}`"
							class="shortcut-section-item__spacer">
							{{ t('calendar', 'or') }}
						</span>
					</template>
				</span>
				<span class="shortcut-section-item__label">{{ shortcut.label }}</span>
			</div>
		</section>
	</Modal>
</template>

<script>
import { translate as t } from '@nextcloud/l10n'
import Modal from '@nextcloud/vue/dist/Components/Modal'

export default {
	components: {
		Modal,
	},
	computed: {
		shortcuts() {
			return [{
				categoryId: 'navigation',
				categoryLabel: t('calendar', 'Navigation'),
				shortcuts: [{
					keys: [['p'], ['k']],
					label: t('calendar', 'Previous period'),
				}, {
					keys: [['n'], ['j']],
					label: t('calendar', 'Next period'),
				}, {
					keys: [['t']],
					label: t('calendar', 'Today'),
				}],
			}, {
				categoryId: 'views',
				categoryLabel: t('calendar', 'Views'),
				shortcuts: [{
					keys: [['1'], ['d']],
					label: t('calendar', 'Day view'),
				}, {
					keys: [['2'], ['w']],
					label: t('calendar', 'Week view'),
				}, {
					keys: [['3'], ['m']],
					label: t('calendar', 'Month view'),
				}],
			}, {
				categoryId: 'actions',
				categoryLabel: t('calendar', 'Actions'),
				shortcuts: [{
					keys: [['c']],
					label: t('calendar', 'Create event'),
				}, {
					keys: [['h']],
					label: t('calendar', 'Show shortcuts'),
				}],
			}]
		},
	},
}
</script>
