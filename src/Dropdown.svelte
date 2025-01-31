<script lang="ts">
  import { DropdownMenu } from "bits-ui";
  import { Check, Ellipsis } from "lucide-svelte";
  import { fly } from "svelte/transition";

  let isChecked = $state(false);

  function handleToggle(e: MouseEvent) {
    e?.stopPropagation();
    isChecked = !isChecked;
  }

  function handleAction(action: string, e?: Event) {
    e?.stopPropagation();
    if (action === "toggle") {
      isChecked = !isChecked;
    } else {
      console.log("Action clicked:", action);
    }
  }
</script>

<div
  class="flex items-center justify-between p-4 border-b border-gray-200 dark:border-gray-700"
>
  <div class="flex items-center gap-4">
    <span class="text-base text-gray-900 dark:text-white">Test Item</span>
    <button
      class="flex items-center justify-center w-8 h-8 rounded-full hover:bg-gray-100 dark:hover:bg-gray-800"
      onclick={handleToggle}
    >
      <Check
        class={`h-5 w-5 ${isChecked ? "text-primary" : "text-gray-400"}`}
      />
    </button>
  </div>

  <DropdownMenu.Root>
    <DropdownMenu.Trigger
      class="flex items-center justify-center w-8 h-8 rounded-full text-gray-500 hover:bg-gray-100 dark:text-gray-400 dark:hover:bg-gray-800"
      onclick={(e) => e.stopPropagation()}
    >
      <Ellipsis class="h-5 w-5" />
    </DropdownMenu.Trigger>
    <DropdownMenu.Portal>
      <DropdownMenu.Content
        class="z-50 min-w-[200px] rounded-lg border border-gray-200 bg-white p-1 shadow-lg dark:border-gray-700 dark:bg-gray-800"
        forceMount
      >
        {#snippet child({ wrapperProps, props, open })}
          {#if open}
            <div {...wrapperProps}>
              <div {...props} transition:fly>
                <DropdownMenu.Item
                  class="flex w-full items-center rounded-md px-3 py-2 text-sm text-gray-700 hover:bg-gray-100 dark:text-gray-300 dark:hover:bg-gray-700"
                  onSelect={(e) => {
                    e?.stopPropagation?.();
                    handleAction("toggle", e);
                  }}
                >
                  {isChecked ? "Mark Unread" : "Mark Read"}
                </DropdownMenu.Item>
                <DropdownMenu.Item
                  class="flex w-full items-center rounded-md px-3 py-2 text-sm text-gray-700 hover:bg-gray-100 dark:text-gray-300 dark:hover:bg-gray-700"
                  onSelect={(e) => {
                    e?.stopPropagation?.();
                    handleAction("action2", e);
                  }}
                >
                  Action 2
                </DropdownMenu.Item>
                <DropdownMenu.Item
                  class="flex w-full items-center rounded-md px-3 py-2 text-sm text-gray-700 hover:bg-gray-100 dark:text-gray-300 dark:hover:bg-gray-700"
                  onSelect={(e) => {
                    e?.stopPropagation?.();
                    handleAction("action3", e);
                  }}
                >
                  Action 3
                </DropdownMenu.Item>
              </div>
            </div>
          {/if}
        {/snippet}
      </DropdownMenu.Content>
    </DropdownMenu.Portal>
  </DropdownMenu.Root>
</div>
