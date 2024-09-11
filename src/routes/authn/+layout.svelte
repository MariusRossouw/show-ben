<script>
  import { goto } from "$app/navigation";
  import {
    SessionWatch,
    SideMenu,
    removeLS,
  } from "@stratech-team/svelte-component-library";

  let sessionActive = false;
  /**
   * @type {Array<any>}
   */
  let menuItems = [
    {
      label: "Dashboard",
      componentId: "dashboard",
      goto: "/authn/dashboard",
      subMenu: [],
    },
    {
      label: "Menu-item",
      componentId: "menu-item",
      subMenu: [
        {
          label: "Sub-menu-item",
          componentId: "sub-menu-item",
          goto: "/authn/dashboard",
          subMenu: [],
        },
      ],
    },
  ];

  function signOutHandler() {
    removeLS(import.meta.env.VITE_APP_NAME + "-session");
    removeLS(import.meta.env.VITE_APP_NAME + "-user-login-response");
    goto("/");
  }
</script>

<!-- Popup dialog notify when session time is about to expire -->
<SessionWatch bind:sessionActive />
<!-- app content including menu  -->
<div class="desktop-page-layout">
  {#if sessionActive === true}
    <!-- side menu  -->
    <div class="desktop-side-menu-container">
      <SideMenu
        {menuItems}
        activeComponentID={"dashboard"}
        menuName={"Console-Products"}
        on:sideMenuLogoutClicked={signOutHandler}
      />
    </div>
    <!-- App content goes into this slot -->
    <slot />
  {/if}
</div>
