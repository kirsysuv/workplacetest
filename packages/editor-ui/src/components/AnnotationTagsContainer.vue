<script lang="ts" setup>
import { computed, defineProps, defineEmits } from 'vue';
import TagsContainer from './TagsContainer.vue';
import { useAnnotationTagsStore } from '@/stores/tags.store';
import type { ITag } from '@/Interface';

interface Props {
	tagIds: string[];
	limit?: number;
	clickable?: boolean;
	responsive?: boolean;
	hoverable?: boolean;
}

defineProps<Props>();

const emit = defineEmits<{
	click: [tagId: string];
}>();

const annotationTagsStore = useAnnotationTagsStore();

const tagsById = computed<Record<string, ITag>>(() => annotationTagsStore.tagsById);

function onClick(tagId: string) {
	emit('click', tagId);
}
</script>

<template>
	<TagsContainer
		:tag-ids="tagIds"
		:tags-by-id="tagsById"
		:limit="limit"
		:clickable="clickable"
		:responsive="responsive"
		:hoverable="hoverable"
		@click="onClick"
	/>
</template>
