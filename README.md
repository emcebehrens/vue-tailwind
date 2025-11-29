# Vue 3 + TypeScript + Vite + Tailwind

There are 5 branches, and they build on each other in this sequence:
- master
- tailwind-first-steps
- light-dark
- tailwind-showcase
- sidepanel

Looking at the draft PRs in github is a quick way to see how the branches build on each other.

## master
Created with:

npm create vite@latest PROJECT_NAME --template vue-ts

## tailwind-first-steps

Add Tailwind :

npm install tailwindcss @tailwindcss/vite

Then add tailwind plugin in vite.config.ts :

Add @import "tailwindcss"; in style.css

## light-dark
Toggle light and dark theme from header

## tailwind-showcase
Using tailwind and css in various ways.

## sidepanel
Sidepanel using css and tailwind
