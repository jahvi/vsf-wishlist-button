<template>
  <button type="button" class="root" :class="{ active: isOnWishlist }" @click="isOnWishlist ? removeFromWishlist(product) : addToWishlist(product)" data-testid="addToWishlist">
    <svg width="18" height="16" viewBox="0 0 18 16">
      <path
        d="M9.01163699,14.9053769 C8.72930024,14.7740736 8.41492611,14.6176996 8.07646224,14.4366167 C7.06926649,13.897753 6.06198912,13.2561336 5.12636931,12.5170512 C2.52930452,10.4655288 1.00308384,8.09476443 1.00000218,5.44184117 C0.997549066,2.99198843 2.92175104,1.01242822 5.28303025,1.01000225 C6.41066623,1.00972036 7.49184369,1.4629765 8.28270844,2.2678673 L8.99827421,2.9961237 L9.71152148,2.26559643 C10.4995294,1.45849728 11.5791258,1.0023831 12.7071151,1.00000055 L12.7060299,1.00000225 C15.0693815,0.997574983 16.9967334,2.97018759 17.0000037,5.421337 C17.0038592,8.07662382 15.4809572,10.4530151 12.8850542,12.5121483 C11.9520963,13.2521931 10.9477036,13.8951276 9.94340074,14.4354976 C9.60619585,14.6169323 9.29297309,14.7736855 9.01163699,14.9053769 Z"
        stroke="#2D2D2D"
        stroke-width="2"
        fill="transparent"
      />
    </svg>
    <span
      class="smallHeart"
      :style="{
        '--translateX': generateCoordinate(),
        '--translateY': generateCoordinate()
      }"
    />
    <span
      class="smallHeart"
      :style="{
        '--translateX': generateCoordinate(),
        '--translateY': generateCoordinate()
      }"
    />
  </button>
</template>

<script>
  import { IsOnWishlist } from '@vue-storefront/core/modules/wishlist/components/IsOnWishlist'
  import { AddToWishlist } from '@vue-storefront/core/modules/wishlist/components/AddToWishlist'
  import { RemoveFromWishlist } from '@vue-storefront/core/modules/wishlist/components/RemoveFromWishlist'

  export default {
    mixins: [IsOnWishlist, AddToWishlist, RemoveFromWishlist],
    methods: {
      generateCoordinate: () => {
        let coordinate = Math.floor(Math.random() * 20) + 5
        coordinate *= Math.floor(Math.random() * 2) === 1 ? 1 : -1

        return coordinate
      }
    }
  }
</script>

<style lang="scss" scoped>
  .root {
    position: relative;
    height: 36px;
    width: 36px;
    padding: 11px 8px 8px;
    cursor: pointer;
    color: #2d2d2d;
    outline: none;
    border: none;
    border-radius: 50%;
    background-color: hsla(0, 0%, 100%, 0.8);
    box-shadow: 0 2px 4px 0 rgba(45, 45, 45, 0.14);

    path {
      transition: fill 0.3s;
    }
  }

  .active {
    path {
      fill: #2d2d2d;
    }

    svg {
      animation: beat cubic-bezier(0.04, 0.4, 0.5, 0.95) 1.2s forwards 1;
    }

    .smallHeart {
      animation: floatAway ease-out 2s forwards 1;
    }
  }

  @keyframes beat {
    30% {
      transform: scale(1.4);
    }

    50% {
      transform: scale(0.8);
    }

    100% {
      transform: scale(1);
    }
  }

  .smallHeart {
    position: absolute;
    top: 50%;
    left: 50%;
    height: 20px;
    width: 20px;
    margin: -10px 0 0 -10px;
    opacity: 0;
    pointer-events: none;
    background: url("data:image/svg+xml;charset=utf-8,%3Csvg width='7' height='6' viewBox='0 0 18 16' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M9.012 14.905a19.999 19.999 0 0 1-3.885-2.388C2.528 10.466 1.002 8.095 1 5.442c-.002-2.45 1.922-4.43 4.283-4.432 1.128 0 2.209.453 3 1.258l.715.728.714-.73A4.199 4.199 0 0 1 12.707 1h-.001C15.069.998 16.996 2.97 17 5.421c.004 2.656-1.519 5.032-4.115 7.091a20.008 20.008 0 0 1-3.873 2.393z' stroke='%232D2D2D' stroke-width='2' fill='%232d2d2d'/%3E%3C/svg%3E");
    background-position: 50%;
    background-repeat: no-repeat;
  }

  @keyframes floatAway {
    15% {
      opacity: 0;
    }

    16% {
      opacity: 1;
      transform: translate(0, 0);
    }

    100% {
      transform: translate(
        calc(var(--translateX) * 1px),
        calc(var(--translateY) * 1px)
      );
      opacity: 0;
    }
  }
</style>
