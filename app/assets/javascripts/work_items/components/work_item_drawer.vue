<script>
import { GlLink, GlDrawer } from '@gitlab/ui';
import { escapeRegExp } from 'lodash';
import deleteWorkItemMutation from '~/work_items/graphql/delete_work_item.mutation.graphql';
import * as Sentry from '~/sentry/sentry_browser_wrapper';
import { visitUrl } from '~/lib/utils/url_utility';

export default {
  name: 'WorkItemDrawer',
  components: {
    GlLink,
    GlDrawer,
    WorkItemDetail: () => import('~/work_items/components/work_item_detail.vue'),
  },
  inject: ['fullPath'],
  inheritAttrs: false,
  props: {
    open: {
      type: Boolean,
      required: true,
    },
    activeItem: {
      type: Object,
      required: false,
      default: () => ({}),
    },
  },
  computed: {
    activeItemFullPath() {
      return this.activeItem?.fullPath;
    },
  },
  methods: {
    async deleteWorkItem({ workItemId }) {
      try {
        const { data } = await this.$apollo.mutate({
          mutation: deleteWorkItemMutation,
          variables: { input: { id: workItemId } },
        });
        if (data.workItemDelete.errors?.length) {
          throw new Error(data.workItemDelete.errors[0]);
        }
        this.$emit('workItemDeleted');
      } catch (error) {
        this.$emit('deleteWorkItemError');
        Sentry.captureException(error);
      }
    },
    redirectToWorkItem() {
      const workItem = this.activeItem;
      const escapedFullPath = escapeRegExp(this.fullPath);
      // eslint-disable-next-line no-useless-escape
      const regex = new RegExp(`groups\/${escapedFullPath}\/-\/(work_items|epics)\/\\d+`);
      const isWorkItemPath = regex.test(workItem.webUrl);

      if (isWorkItemPath) {
        this.$router.push({
          name: 'workItem',
          params: {
            iid: workItem.iid,
          },
        });
      } else {
        visitUrl(workItem.webUrl);
      }
    },
  },
};
</script>

<template>
  <gl-drawer
    :open="open"
    data-testid="work-item-drawer"
    header-height="calc(var(--top-bar-height) + var(--performance-bar-height))"
    class="gl-w-full gl-sm-w-40p gl-leading-reset"
    @close="$emit('close')"
  >
    <template #title>
      <gl-link
        class="gl-text-black-normal"
        :href="activeItem.webUrl"
        @click.prevent="redirectToWorkItem"
        >{{ __('Open full view') }}</gl-link
      >
    </template>
    <template #default>
      <work-item-detail
        :key="activeItem.iid"
        :work-item-iid="activeItem.iid"
        :modal-work-item-full-path="activeItemFullPath"
        is-drawer
        class="gl-pt-0! work-item-drawer"
        @deleteWorkItem="deleteWorkItem"
        v-on="$listeners"
      />
    </template>
  </gl-drawer>
</template>
