<template>
  <ul class="flex gap-3 text-sm">
    <li class="inline-flex items-center gap-2">
      <StockIndicator availability="available" /> Available
    </li>
    <li class="inline-flex items-center gap-2">
      <StockIndicator availability="low" /> Low in stock
    </li>
    <li class="inline-flex items-center gap-2">
      <StockIndicator availability="unavailable" /> Out of stock
    </li>
  </ul>
</template>
