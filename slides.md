---
theme: default
title: HTML Basics for Beginners
transition: slide-left
highlighter: shiki
fonts:
  mono: Consolas
---

# HTML Basics

### Building blocks of every web page

---
layout: default
---

# What is HTML?

<v-clicks>

- **H**yper**T**ext **M**arkup **L**anguage
- Describes the *structure* of a web page and its content
- Made of **elements** built from **tags**

</v-clicks>

---
layout: default
clicks: 3
---

# The Keys You'll Need

<div class="mt-6 flex justify-center">
  <KeyboardLayout :keys="[
    { id: 'comma',  needShift: true,  hlChar: '<' },
    { id: 'period', needShift: true,  hlChar: '>' },
    { id: 'slash',  needShift: false, hlChar: '/' },
  ]" />
</div>

<div class="mt-5 text-center text-sm grid">
  <div v-click="[1, 2]" v-motion :initial="{ opacity: 0, y: 8 }" :enter="{ opacity: 1, y: 0 }" :leave="{ opacity: 0, y: -8 }" class="text-yellow-700 dark:text-yellow-400 font-bold text-base" style="grid-area: 1/1">
    <div class="text-white font-normal">open angle bracket, less than</div>
    <span class="border-1 p-1 px-2 rounded">Shift</span> + <span class="font-mono border-1 px-2 py-1 rounded">,</span> <span class="text-white text-2xl font-normal">&nbsp;→&nbsp;</span><span class="font-mono text-xl">&lt;</span>
  </div>
  <div v-click="[2, 3]" v-motion :initial="{ opacity: 0, y: 8 }" :enter="{ opacity: 1, y: 0 }" :leave="{ opacity: 0, y: -8 }" class="text-yellow-700 dark:text-yellow-400 font-bold text-base" style="grid-area: 1/1">
    <div class="text-white font-normal">close angle bracket, greater than</div>
    <span class="border-1 p-1 px-2 rounded">Shift</span> + <span class="font-mono border-1 px-2 py-1 rounded">.</span> <span class="text-white text-2xl font-normal">&nbsp;→&nbsp;</span><span class="font-mono text-xl">&gt;</span>
  </div>
  <div v-click="[3, 4]" v-motion :initial="{ opacity: 0, y: 8 }" :enter="{ opacity: 1, y: 0 }" :leave="{ opacity: 0, y: -8 }" class="text-yellow-700 dark:text-yellow-400 font-bold text-base" style="grid-area: 1/1">
    <div class="text-white font-normal"><span class="font-bold">slash</span>, <span class="font-bold">forward slash</span>, diagonal, solidus</div>
    <span class="font-mono border-1 px-2 py-1 rounded">/</span> <span class="text-white text-2xl font-normal">&nbsp;→&nbsp;</span><span class="font-mono text-xl">/</span> <span class="text-gray-500 font-normal">(no Shift needed)</span>
  </div>
</div>

---
layout: default
clicks: 4
---

# Building a Start Tag

<div class="mt-8">
  <TagBuilder tag-name="h1" :start-at="1" />
</div>

<div class="mt-8 flex flex-col gap-2 text-2xl text-gray-500 dark:text-gray-400 items-start w-72 mx-auto">
  <span v-click="1" class="click-label">① opening bracket <span class="text-blue-600 dark:text-blue-400">&lt;</span></span>
  <span v-click="2" class="click-label">② tag name</span>
  <span v-click="3" class="click-label">③ closing bracket <span class="text-blue-600 dark:text-blue-400">&gt;</span></span>
  <span v-click="4" class="click-label">No space between opening bracket and tag name!</span>
</div>

---
layout: default
clicks: 5
---

# Building the End Tag

<div class="mt-8">
  <TagBuilder tag-name="h1" :closing="true" :start-at="1" />
</div>

<div class="mt-8 flex flex-col gap-2 text-2xl items-start w-72 mx-auto">
  <span v-click="1" class="text-gray-500 dark:text-gray-400 click-label">① opening bracket<span class="text-blue-600 dark:text-blue-400">&lt;</span></span>
  <span v-click="2" class="text-orange-600 dark:text-orange-400 click-label ">② the slash /</span>
  <span v-click="3" class="text-gray-500 dark:text-gray-400 click-label">③ tag name</span>
  <span v-click="4" class="text-gray-500 dark:text-gray-400 click-label">④ closing bracket <span class="text-blue-600 dark:text-blue-400">&gt;</span></span>
    <span v-click="45" class="click-label">No space between opening bracket, /, tag name, and closing bracket!</span>
</div>

---
layout: center
clicks: 4
---

# A Complete Element

start tag + content + end tag = element

<div class="relative mt-10 pb-10">

  <!-- Code row -->
  <div class="font-mono flex items-end justify-center gap-1 text-4xl select-none">
    <!-- Start tag (click 1) springs in from left -->
    <div
      v-click="1"
      v-motion
      :initial="{ opacity: 0, x: -60 }"
      :enter="{ opacity: 1, x: 0, transition: { type: 'spring', stiffness: 100, damping: 15 } }"
      class="flex flex-col items-center gap-2"
    >
      <span class="text-blue-600 dark:text-blue-400">&lt;h1&gt;</span>
      <div class="w-full border-b-2 border-blue-600 dark:border-blue-400"></div>
      <span class="font-sans text-base text-blue-600 dark:text-blue-400">start tag</span>
    </div>
    <!-- Content (click 3)  drops in from above -->
    <div
      v-click="3"
      v-motion
      :initial="{ opacity: 0, y: -30 }"
      :enter="{ opacity: 1, y: 0, transition: { duration: 400 } }"
      class="flex flex-col items-center gap-2"
    >
      <span class="text-green-700 dark:text-green-300">Hello, World!</span>
      <div class="w-full border-b-2 border-green-700 dark:border-green-300"></div>
      <span class="font-sans text-base text-green-700 dark:text-green-300">content</span>
    </div>
    <!-- End tag (click 2) springs in from right -->
    <div
      v-click="2"
      v-motion
      :initial="{ opacity: 0, x: 60 }"
      :enter="{ opacity: 1, x: 0, transition: { type: 'spring', stiffness: 100, damping: 15 } }"
      class="flex flex-col items-center gap-2"
    >
      <span class="text-blue-600 dark:text-blue-400">&lt;/h1&gt;</span>
      <div class="w-full border-b-2 border-blue-600 dark:border-blue-400"></div>
      <span class="font-sans text-base text-blue-600 dark:text-blue-400">end tag</span>
    </div>
  </div>

  <!-- Spanning "element" underline (click 4) -->
  <div
    v-click="4"
    v-motion
    :initial="{ opacity: 0 }"
    :enter="{ opacity: 1, transition: { duration: 500 } }"
    class="absolute inset-x-0 bottom-2 flex items-center gap-3 text-gray-500 dark:text-gray-400"
  >
    <div class="flex-1 border-b-2 border-gray-400 dark:border-gray-500"></div>
    <span class="text-sm whitespace-nowrap">element</span>
    <div class="flex-1 border-b-2 border-gray-400 dark:border-gray-500"></div>
  </div>

</div>

---
layout: default
clicks: 6
---

# Elements Inside Elements

<div class="mt-6 flex justify-center">
  <NestingDemo />
</div>

<div
  v-click="6"
  v-motion
  :initial="{ opacity: 0, y: 10 }"
  :enter="{ opacity: 1, y: 0 }"
  class="mt-6 text-center text-sm text-gray-500 dark:text-gray-400"
>
  the <span class="text-blue-600 dark:text-blue-400">li</span> elements are <em>children</em> of <span class="text-purple-500">ul</span> — nested inside, balanced inside
</div>

---
layout: default
clicks: 6
---

# Attributes Add Information

<div class="font-mono text-4xl mt-8 text-left whitespace-nowrap"><!--
  --><span v-click="1" class="text-blue-600 dark:text-blue-400">&lt;</span><!--
  --><span v-click="2" class="text-gray-800 dark:text-gray-200">a</span><!--
  --><span v-click="3" v-motion :initial="{ opacity: 0, x: -20 }" :enter="{ opacity: 1, x: 0 }" class="text-yellow-700 dark:text-yellow-300 inline-block">&nbsp;href</span><!--
  --><span v-click="4" v-motion :initial="{ opacity: 0, x: -20 }" :enter="{ opacity: 1, x: 0 }" class="text-green-700 dark:text-green-300 inline-block">="https://www.harvard.edu/"</span><!--
  --><span v-click="5" class="text-blue-600 dark:text-blue-400">&gt;</span><!--
--></div>
<div v-click="6" v-motion :initial="{ opacity: 0, x: -20 }" :enter="{ opacity: 1, x: 0 }" class="font-mono text-4xl mt-4 text-left whitespace-nowrap"><!--
--><span class="text-gray-400">Harvard University</span><!--
  --><span class="text-blue-600 dark:text-blue-400">&lt;<span class="text-orange-400">/</span><span class="text-gray-800 dark-text-gray-200">a</span>&gt;</span><!--
--></div>
<div class="mt-8 flex flex-col gap-4 text-lg justify-center">
  <span v-click="2" class="text-yellow-700 dark:text-yellow-300">attribute name</span>
  <span v-click="3" class="text-green-700 dark:text-green-300">attribute value</span>
  <span v-click="4">attributes are part of the start tag!</span>
</div>


---
layout: default
---

# You now know:

<v-clicks>

- What HTML tags look like: `<tagname>` and `</tagname>`
- That every start tag has a matching end tag
- How attributes (`name="value"`) add extra information
- That a complete **element** = start tag + content + end tag

</v-clicks>
