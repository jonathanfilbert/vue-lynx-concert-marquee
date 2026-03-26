# Vue-Lynx Concert Marquee

A sleek concert-style marquee display application built with Vue 3 and Lynx. Create eye-catching scrolling text with customizable themes and animation speeds.

<img width="1268" height="911" alt="image" src="https://github.com/user-attachments/assets/4928b3ec-8e36-4c12-b487-5f50d671d921" />

## Features

- **Custom Themes**: Three pre-built themes - Concert (red), Neon (cyan), and Sunset (orange)
- **Adjustable Speed**: Control marquee scrolling speed (3-10 seconds per cycle)
- **Smooth Animations**: Hardware-accelerated CSS animations for fluid text scrolling
- **Lynx Integration**: Built with vue-lynx for cross-platform compatibility

## Tech Stack

- [Vue 3](https://vuejs.org/) - Progressive JavaScript framework
- [vue-lynx](https://github.com/lynx-family/vue-lynx) - Vue integration for Lynx framework
- [TypeScript](https://www.typescriptlang.org/) - Type-safe development
- [@lynx-js/rspeedy](https://github.com/lynx-family/rspeedy) - Build tool based on Rsbuild

## Getting Started

### Prerequisites

- Node.js >= 18

### Installation

```bash
npm install
```

### Development

```bash
npm run dev
```

Scan the QRCode displayed in the terminal with your LynxExplorer App to view the application.

### Build

```bash
npm run build
```

### Preview

```bash
npm run preview
```

## View Demo with Lynx Explorer

You can view the demo without running a local development server:

1. **Download Lynx Explorer** from the [Lynx Quick Start Guide](https://lynxjs.org/rspeedy/start/quick-start?ios-simulator-platform=macos-arm64&explorer-platform=ios-simulator#prepare-lynx-explorer)

2. **Open Lynx Explorer** and paste this bundle URL:

```
https://github.com/jonathanfilbert/vue-lynx-concert-marquee/raw/refs/heads/main/dist/main.lynx.bundle
```

## Scripts

| Command | Description |
|---------|-------------|
| `npm run dev` | Start development server with hot reload |
| `npm run build` | Build for production |
| `npm run preview` | Preview production build |
| `npm run lint` | Run ESLint |
| `npm run format` | Format code with Prettier |

## Project Structure

```
src/
├── App.vue          # Main application component
├── App.css          # Global styles
├── index.ts         # Application entry point
├── lib/             # Utility functions
└── assets/          # Static assets
```

## Configuration

- **lynx.config.ts** - Lynx/Rspeedy build configuration
- **tsconfig.json** - TypeScript compiler options
- **.prettierrc** - Code formatting rules
- **eslint.config.mjs** - ESLint linting rules

## License

Private
