<script lang="ts">
  import "../app.postcss";
  import {
    AppShell,
    AppBar,
    LightSwitch,
    initializeStores,
    Modal,
    type ModalComponent,
  } from "@skeletonlabs/skeleton";
  import { base } from "$app/paths";
  import { version } from "$app/environment";
  import { GitHubIcon } from "$lib/icons";
  import { ScreenWakeLock } from "$lib/components";
  import { AtomicCounterModal, CounterModal } from "$lib/modals";

  initializeStores();

  const title = "DeltaCount";

  const modalRegistry: Record<string, ModalComponent> = {
    atomicCounter: { ref: AtomicCounterModal },
    counter: { ref: CounterModal },
  };
</script>

<svelte:head>
  <title>{title}</title>
</svelte:head>

<ScreenWakeLock />

<Modal components={modalRegistry} />

<!-- App Shell -->
<AppShell>
  <svelte:fragment slot="header">
    <!-- App Bar -->
    <AppBar>
      <svelte:fragment slot="lead">
        <a href="{base}/">
          <strong class="text-xl uppercase">{title}</strong>
        </a>
      </svelte:fragment>
      <svelte:fragment slot="trail">
        <LightSwitch />
        <a
          class="btn btn-icon variant-ghost-surface"
          href="https://github.com/srtigers98/deltacount"
          target="_blank"
          rel="noreferrer"
        >
          <GitHubIcon />
        </a>
      </svelte:fragment>
    </AppBar>
  </svelte:fragment>
  <!-- Page Route Content -->
  <div class="mb-10 h-full w-full flex justify-center items-center">
    <div class="w-4/5 space-y-10 text-center flex flex-col items-center">
      <slot />
    </div>
  </div>
  <svelte:fragment slot="footer">
    <AppBar>
      <svelte:fragment slot="lead"><div></div></svelte:fragment>
      <svelte:fragment slot="trail">
        <span class="chip bg-gradient-to-br variant-gradient-secondary-primary cursor-default"
          >{version}</span
        >
      </svelte:fragment>
    </AppBar>
  </svelte:fragment>
</AppShell>
