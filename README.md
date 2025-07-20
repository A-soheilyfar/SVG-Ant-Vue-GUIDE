# SVG-Ant-Vue-GUIDE


I found the correct and most modern way to handle custom SVGs in a Vite-based Ant Design Vue project. Your solution is spot-on.

Here's a summary of your method, structured for clarity.

Solution: Using Custom SVGs in Ant Design Vue Tree
This method uses Vite's built-in feature to import SVGs directly as Vue components.

⚙️ Step 1: Configure TypeScript for SVG Imports
For TypeScript to understand the special ?component import, you need to declare the module type.

In your vite-env.d.ts file, add the following declaration:

/// <reference types="vite/client" />

// This tells TypeScript how to handle '.svg?component' imports
declare module '*.svg?component' {
  import { DefineComponent } from 'vue';
  const component: DefineComponent;
  export default component;
}
✅ Step 2: Import SVGs as Components
In your Vue component's <script> section, import your SVG files by appending ?component to the file path. This tells Vite to load them as Vue components.



<script lang="ts" setup>
import { ref } from 'vue';
import type { TreeProps } from 'ant-design-vue';
// Import SVG icons as components
import FolderOpenIcon from '@/assets/icons/gui-folder-open.svg?component';
import FolderCloseIcon from '@/assets/icons/gui-folder.svg?component';
const expandedKeys = ref<string[]>(['0-0-0']);
// ... other script setup code
</script>
🎨 Step 3: Use the Icons in the a-tree Template

Use the #switcherIcon slot provided by the a-tree component. This slot gives you access to properties like expanded and isLeaf, allowing you to conditionally render the correct icon.

<template>
  <a-tree
    v-model:expandedKeys="expandedKeys"
    v-model:selectedKeys="selectedKeys"
    show-line
    :tree-data="treeData"
  >
    <template #switcherIcon="{ expanded }">
      <FolderOpenIcon v-if="expanded" />
      <FolderCloseIcon v-else />
    </template>
  </a-tree>
</template>
This is the best practice for this scenario because it's clean, efficient, and leverages modern build tool features without requiring extra wrapper components.

I hope you use it and like it this is my result
I use that to change folder SVG Icons
