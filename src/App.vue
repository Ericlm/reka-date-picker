<script setup lang="ts">
import {
  DateRangePickerArrow,
  DateRangePickerCalendar,
  DateRangePickerCell,
  DateRangePickerCellTrigger,
  DateRangePickerContent,
  DateRangePickerField,
  DateRangePickerGrid,
  DateRangePickerGridBody,
  DateRangePickerGridHead,
  DateRangePickerGridRow,
  DateRangePickerHeadCell,
  DateRangePickerHeader,
  DateRangePickerHeading,
  DateRangePickerInput,
  DateRangePickerNext,
  DateRangePickerPrev,
  DateRangePickerRoot,
  DateRangePickerTrigger,
  DatePickerRoot,
  DatePickerField,
  DatePickerInput,
  DatePickerTrigger,
  DatePickerContent,
  DatePickerArrow,
  DatePickerCalendar,
  DatePickerHeader,
  DatePickerPrev,
  DatePickerHeading,
  DatePickerNext,
  DatePickerGrid,
  DatePickerGridHead,
  DatePickerGridRow,
  DatePickerHeadCell,
  DatePickerGridBody,
  DatePickerCell,
  DatePickerCellTrigger
} from 'reka-ui'
</script>

<template>
  <div class="flex flex-col p-20 gap-y-10">
    <DateRangePickerRoot
      id="booking"
      :is-date-unavailable="date => date.day === 19"
      as="span"
      class="bg-pink-500"
    >
      <DateRangePickerField
        v-slot="{ segments }"
        class="flex select-none bg-white items-center rounded-lg text-center text-green10 border shadow-sm p-1 data-[invalid]:border-red-500"
      >
        <template
          v-for="item in segments.start"
          :key="item.part"
        >
          <DateRangePickerInput
            v-if="item.part === 'literal'"
            :part="item.part"
            type="start"
          >
            {{ item.value }}
          </DateRangePickerInput>
          <DateRangePickerInput
            v-else
            :part="item.part"
            class="rounded-md p-0.5 focus:outline-none focus:shadow-[0_0_0_2px] focus:shadow-black data-[placeholder]:text-green9"
            type="start"
          >
            {{ item.value }}
          </DateRangePickerInput>
        </template>
        <span class="mx-2">

          -
        </span>
        <template
          v-for="item in segments.end"
          :key="item.part"
        >
          <DateRangePickerInput
            v-if="item.part === 'literal'"
            :part="item.part"
            type="end"
          >
            {{ item.value }}
          </DateRangePickerInput>
          <DateRangePickerInput
            v-else
            :part="item.part"
            class="rounded-md p-0.5 focus:outline-none focus:shadow-[0_0_0_2px] focus:shadow-black data-[placeholder]:text-green9"
            type="end"
          >
            {{ item.value }}
          </DateRangePickerInput>
        </template>

        <DateRangePickerTrigger class="ml-4 bg-amber-200 focus:shadow-[0_0_0_2px] focus:shadow-black focus:outline-none rounded p-1">
          TRIGGER
        </DateRangePickerTrigger>
      </DateRangePickerField>

      <DateRangePickerContent
        :side-offset="4"
        class="rounded-xl bg-white border shadow-sm will-change-[transform,opacity] data-[state=open]:data-[side=top]:animate-slideDownAndFade data-[state=open]:data-[side=right]:animate-slideLeftAndFade data-[state=open]:data-[side=bottom]:animate-slideUpAndFade data-[state=open]:data-[side=left]:animate-slideRightAndFade"
      >
        <DateRangePickerArrow class="fill-white stroke-gray-300" />
        <DateRangePickerCalendar
          v-slot="{ weekDays, grid }"
          class="p-4"
        >
          <DateRangePickerHeader class="flex items-center justify-between">
            <DateRangePickerPrev
              class="inline-flex items-center cursor-pointer text-black justify-center rounded-md bg-transparent w-7 h-7 hover:bg-stone-100 active:scale-98 active:transition-all focus:shadow-[0_0_0_2px] focus:shadow-black"
            >
              PREV
            </DateRangePickerPrev>

            <DateRangePickerHeading class="text-sm text-black font-medium" />
            <DateRangePickerNext
              class="inline-flex items-center cursor-pointer text-black justify-center rounded-md bg-transparent w-7 h-7 hover:bg-stone-100 active:scale-98 active:transition-all focus:shadow-[0_0_0_2px] focus:shadow-black"
            >
              NEXT
            </DateRangePickerNext>
          </DateRangePickerHeader>
          <div
            class="flex flex-col space-y-4 pt-4 sm:flex-row sm:space-x-4 sm:space-y-0"
          >
            <DateRangePickerGrid
              v-for="month in grid"
              :key="month.value.toString()"
              class="w-full border-collapse select-none space-y-1"
            >
              <DateRangePickerGridHead>
                <DateRangePickerGridRow class="mb-1 flex w-full justify-between">
                  <DateRangePickerHeadCell
                    v-for="day in weekDays"
                    :key="day"
                    class="w-8 rounded-md text-xs font-normal! text-black"
                  >
                    {{ day }}
                  </DateRangePickerHeadCell>
                </DateRangePickerGridRow>
              </DateRangePickerGridHead>
              <DateRangePickerGridBody>
                <DateRangePickerGridRow
                  v-for="(weekDates, index) in month.rows"
                  :key="`weekDate-${index}`"
                  class="flex w-full"
                >
                  <DateRangePickerCell
                    v-for="weekDate in weekDates"
                    :key="weekDate.toString()"
                    :date="weekDate"
                  >
                    <DateRangePickerCellTrigger
                      :day="weekDate"
                      :month="month.value"
                      class="relative flex items-center justify-center rounded-full whitespace-nowrap text-sm font-normal text-black w-8 h-8 outline-none focus:shadow-[0_0_0_2px] focus:shadow-black data-[outside-view]:text-black/30 data-[selected]:!bg-green10 data-[selected]:text-white hover:bg-green5 data-[highlighted]:bg-green5 data-[unavailable]:pointer-events-none data-[unavailable]:text-black/30 data-[unavailable]:line-through before:absolute before:top-[5px] before:hidden before:rounded-full before:w-1 before:h-1 before:bg-white data-[today]:before:block data-[today]:before:bg-green9 "
                    />
                  </DateRangePickerCell>
                </DateRangePickerGridRow>
              </DateRangePickerGridBody>
            </DateRangePickerGrid>
          </div>
        </DateRangePickerCalendar>
      </DateRangePickerContent>
    </DateRangePickerRoot>

     <DatePickerRoot
      id="birthday"
      as="span"
      class="bg-purple-500"
      :is-date-unavailable="date => date.day === 19"
    >
      <DatePickerField
        v-slot="{ segments }"
        class="flex select-none bg-white items-center rounded-lg shadow-sm text-center justify-between text-green10 border p-1 data-[invalid]:border-red-500"
      >
        <div class="flex items-center">
          <template
            v-for="item in segments"
            :key="item.part"
          >
            <DatePickerInput
              v-if="item.part === 'literal'"
              :part="item.part"
            >
              {{ item.value }}
            </DatePickerInput>
            <DatePickerInput
              v-else
              :part="item.part"
              class="rounded p-0.5 focus:outline-none focus:shadow-[0_0_0_2px] focus:shadow-black data-[placeholder]:text-green9"
            >
              {{ item.value }}
            </DatePickerInput>
          </template>
        </div>

        <DatePickerTrigger class="focus:shadow-[0_0_0_2px] rounded p-1 focus:shadow-black bg-amber-100">
          Trigger
        </DatePickerTrigger>
      </DatePickerField>

      <DatePickerContent
        :side-offset="4"
        class="rounded-xl bg-white border shadow-sm will-change-[transform,opacity] data-[state=open]:data-[side=top]:animate-slideDownAndFade data-[state=open]:data-[side=right]:animate-slideLeftAndFade data-[state=open]:data-[side=bottom]:animate-slideUpAndFade data-[state=open]:data-[side=left]:animate-slideRightAndFade"
      >
        <DatePickerArrow class="fill-white stroke-gray-300" />
        <DatePickerCalendar
          v-slot="{ weekDays, grid }"
          class="p-4"
        >
          <DatePickerHeader class="flex items-center justify-between">
            <DatePickerPrev
              class="inline-flex items-center cursor-pointer text-black justify-center rounded-md bg-transparent w-7 h-7 hover:bg-stone-50 active:scale-98 active:transition-all focus:shadow-[0_0_0_2px] focus:shadow-black"
            >
              PREV
            </DatePickerPrev>

            <DatePickerHeading class="text-black font-medium" />

            <DatePickerNext
              class="inline-flex items-center cursor-pointer text-black justify-center rounded-md bg-transparent w-7 h-7 hover:bg-stone-50 active:scale-98 active:transition-all focus:shadow-[0_0_0_2px] focus:shadow-black"
            >
              NEXT
            </DatePickerNext>
          </DatePickerHeader>
          <div
            class="flex flex-col space-y-4 pt-4 sm:flex-row sm:space-x-4 sm:space-y-0"
          >
            <DatePickerGrid
              v-for="month in grid"
              :key="month.value.toString()"
              class="w-full border-collapse select-none space-y-1"
            >
              <DatePickerGridHead>
                <DatePickerGridRow class="mb-1 flex w-full justify-between">
                  <DatePickerHeadCell
                    v-for="day in weekDays"
                    :key="day"
                    class="w-8 rounded-md text-xs text-green8"
                  >
                    {{ day }}
                  </DatePickerHeadCell>
                </DatePickerGridRow>
              </DatePickerGridHead>
              <DatePickerGridBody>
                <DatePickerGridRow
                  v-for="(weekDates, index) in month.rows"
                  :key="`weekDate-${index}`"
                  class="flex w-full"
                >
                  <DatePickerCell
                    v-for="weekDate in weekDates"
                    :key="weekDate.toString()"
                    :date="weekDate"
                  >
                    <DatePickerCellTrigger
                      :day="weekDate"
                      :month="month.value"
                      class="relative flex items-center justify-center whitespace-nowrap rounded-[9px] border border-transparent bg-transparent text-sm font-normal text-black w-8 h-8 outline-none focus:shadow-[0_0_0_2px] focus:shadow-black hover:border-black data-[selected]:bg-black data-[selected]:font-medium data-[outside-view]:text-black/30 data-[selected]:text-white data-[unavailable]:pointer-events-none data-[unavailable]:text-black/30 data-[unavailable]:line-through before:absolute before:top-[5px] before:hidden before:rounded-full before:w-1 before:h-1 before:bg-white data-[today]:before:block data-[today]:before:bg-green9 data-[selected]:before:bg-white"
                    />
                  </DatePickerCell>
                </DatePickerGridRow>
              </DatePickerGridBody>
            </DatePickerGrid>
          </div>
        </DatePickerCalendar>
      </DatePickerContent>
    </DatePickerRoot>
  </div>
</template>