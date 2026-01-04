# task-frontend

![Project Preview](https://via.placeholder.com/800x400?text=Project+Preview)

## Live Demo

- **Live Site**: [Deploy to Vercel/Netlify]
- **GitHub Repository**: [Your GitHub URL]


## Features

### Section 1: Pinned Slide Transitions
- **Smooth scroll-triggered transitions** between three slides (Plan, Design, Build)
- **Staggered animations** with different timing for each element
- **Advanced effects**: 
  - Scale and blur transitions for slide fade-outs
  - Horizontal slide-in animations for content panels
  - Icon rotation and scale effects
  - Image zoom animations
- **Responsive design** that adapts to mobile, tablet, and desktop

### Section 2: Scale-Up Content Reveal
- **Single card layout** with full-screen images
- **Sequential content reveal**: Empty background → Text appears → Image scales up
- **Three-stage animation** (Plan, Design, Build) with smooth fade transitions
- **Layered effect**: New content scales up and overlays previous content
- **Progress bar indicator** showing scroll progress

### General Features
- **Smooth scroll-linked animations** using GSAP ScrollTrigger
- **Pin effect** that keeps sections in place while animating
- **Optimized performance** with hardware-accelerated transforms
- **Mobile-responsive** with touch-friendly interactions

## 🛠 Technologies Used

### Core Framework
- **Vue.js 2.x** - Progressive JavaScript framework
- **Vue Router** - Official router for Vue.js (if multi-page)

### Animation Libraries
- **GSAP 3.x** - Professional-grade animation library
  - `gsap` - Core animation engine
  - `ScrollTrigger` - Scroll-based animation plugin

### Styling
- **SCSS/Sass** - CSS preprocessor for better styling workflow
- **CSS Grid & Flexbox** - Modern layout systems

### Build Tools
- **Vue CLI** / **Vite** - Modern build tooling
- **Webpack** / **Rollup** - Module bundlers

### Development Tools
- **ESLint** - Code quality and style checking
- **Prettier** - Code formatter

## Project Structure

```
project-root/
├── public/
│   ├── index.html
│   └── favicon.ico
├── src/
│   ├── assets/
│   │   ├── images/
│   │   │   ├── iconPlan.svg
│   │   │   ├── iconDesign.svg
│   │   │   ├── iconBuild.svg
│   │   │   ├── imagePlan.jpg
│   │   │   ├── imageDesign.jpg
│   │   │   └── imageBuild.jpg
│   │   └── styles/
│   │       └── main.scss
│   ├── components/
│   │   ├── header.vue
│   │   └── section-1.vue
│   │   ├── section-2.vue
│   │   └── section-3.vue
│   ├── views/
│   │   └── HomeView.vue
│   │   └── AboutView.vue
│   ├── pages/
│   │   └── index.vue
│   ├── App.vue
│   └── main.js
├── .gitignore
├── package.json
├── README.md
└── vue.config.js (or vite.config.js)
```

## Installation

### Prerequisites
- **Node.js** (v14 or higher)
- **npm** or **yarn**

### Steps

1. **Clone the repository**
```bash
git clone https://github.com/ikaseptiaa/Technical-Test-FE
cd vue-scroll-animation
```

2. **Install dependencies**
```bash
npm install
# or
yarn install
```

3. **Add your assets**
   - Place images in `src/assets/images/`
   - Ensure you have:
     - `iconPlan.svg`, `iconDesign.svg`, `iconBuild.svg`
     - `imagePlan.jpg`, `imageDesign.jpg`, `imageBuild.jpg`

## Development

### Run development server
```bash
npm run serve
# or
yarn serve
```

The app will be available at `http://localhost:8080`

### Hot Module Replacement (HMR)
Changes to your code will automatically reload in the browser.

## Build for Production

```bash
npm run build
# or
yarn build
```

This will create an optimized production build in the `dist/` folder.

### Preview production build locally
```bash
npm run preview
# or
yarn preview
```

## Browser Support

- Chrome (latest)
- Edge (latest)

**Note**: GSAP ScrollTrigger requires modern browser features. IE11 is not supported.

## Key Implementation Details

### GSAP ScrollTrigger Setup

```javascript
import { gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

ScrollTrigger.create({
  trigger: wrapper,
  start: 'top top',
  end: '+=300%',
  pin: container,
  scrub: 1,
  onUpdate: (self) => {
    const progress = self.progress 
  }
})
```

## Author

Ika Septia Anggraeni

## Acknowledgments

- GSAP by GreenSock for amazing animation capabilities
- Vue.js team for the excellent framework
- Design inspiration from modern web portfolios

---

Made with ❤️ and Vue.js
