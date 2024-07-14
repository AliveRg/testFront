<template>
  <svg
    xmlns="http://www.w3.org/2000/svg"
    width="208"
    height="240"
    viewBox="0 0 208 240"
    fill="none"
  >
    <defs>
      <clipPath id="clip">
        <rect width="208" height="240" rx="8" />
      </clipPath>
    </defs>
    <g clip-path="url(#clip)">
      <foreignObject width="208" height="240">
        <slot />
      </foreignObject>
    </g>
    <g filter="url(#filter0_b_4412_10506)">
      <rect width="208" height="240" rx="8" fill="white" fill-opacity="0.1" />
    </g>
    <defs>
      <filter
        id="filter0_b_4412_10506"
        x="-12"
        y="-12"
        width="232"
        height="264"
        filterUnits="userSpaceOnUse"
        color-interpolation-filters="sRGB"
      >
        <feFlood flood-opacity="0" result="BackgroundImageFix" />
        <feGaussianBlur in="BackgroundImageFix" stdDeviation="6" />
        <feComposite in2="SourceAlpha" operator="in" result="effect1_backgroundBlur_4412_10506" />
        <feBlend
          mode="normal"
          in="SourceGraphic"
          in2="effect1_backgroundBlur_4412_10506"
          result="shape"
        />
      </filter>
    </defs>
  </svg>
</template>
