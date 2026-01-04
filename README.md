# Technical Test Frontend – Vue & GSAP

This project is a frontend technical test implementation focusing on scroll-based animations using **Vue.js** and **GSAP (ScrollTrigger)**.  
---

## Project Description

The application consists of multiple sections with scroll-triggered animations:

- **Pinned sections** that stay fixed during scroll  
- **Animated transitions** between content states (Plan, Design, Build)  
- **Smooth scaling, fading, and sliding effects**  
- **Responsive design** for desktop, tablet, and mobile  

The goal of this project is to showcase frontend skills in animation handling, component structure, and clean styling.

---

## Technologies Used

- **Vue.js** – Frontend framework  
- **GSAP** – Animation library  
- **GSAP ScrollTrigger** – Scroll-based animation control  
- **SCSS (Sass)** – Styling and design system  
- **Vite** – Development and build tool  

---

## Project Setup Instructions

### Prerequisites
Make sure you have installed:
- **Node.js** (v14 or higher)
- **npm** or **yarn**

---

### Clone the Repository
```bash
git clone https://github.com/ikaseptiaa/Technical-Test-FE.git
cd Technical-Test-FE
```
### Install Dependencies
```npm install
# or
yarn install
```
### Run the Application
```npm run dev
# or
yarn dev
```
### Build for Production
```npm run build
# or
yarn build
```
### Project Structure
```
src/
├── assets/
│   ├── images/
│   ├── fonts/
│   └── scss/
├── components/
│   ├── header.vue
│   ├── section-1.vue
│   ├── section-2.vue
│   └── section-3.vue
├── pages/
│   └── index.vue
├── App.vue
└── main.js
```
### Additional Features & Considerations
```Uses GSAP ScrollTrigger for scroll synchronization
Pinned animations improve storytelling flow
Hardware-accelerated transforms for better performance
SCSS variables and mixins for consistent design
Clean and reusable Vue components
```
### Author
```
Ika Septia Anggraeni
```
### Acknowledgments
```GSAP for powerful animation tools
Vue.js community for documentation and best practices
```