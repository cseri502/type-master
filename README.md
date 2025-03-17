<p align="center">
	<img src="https://github.com/cseri502/type-master/blob/main/public/typewriter.png" width="128" title="Type Master">
</p>

<h1 align="center">Type Master</h1>

## 📒 Description

A sleek and minimalist typing test application built with Vue, designed to help users improve their typing speed and accuracy. Challenge yourself with quotes of varying difficulty levels and track your progress with real-time metrics.

## 🚀 Technologies & Tools

![Vue](https://img.shields.io/badge/Vue.js-35495E?style=for-the-badge&logo=vue.js&logoColor=4FC08D)
![TypeScript](https://img.shields.io/badge/typescript-%23007ACC.svg?style=for-the-badge&logo=typescript&logoColor=white)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white)
![Axios](https://img.shields.io/badge/Axios-5A29E4?style=for-the-badge&logo=axios&logoColor=white)
<br />
![HTML](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)
![Git](https://img.shields.io/badge/GIT-E44C30?style=for-the-badge&logo=git&logoColor=white)

## ✨ Features

- **Multiple Difficulty Levels**: Choose between easy, medium, and hard difficulty settings
- **Real-time Metrics**: Track your typing speed (WPM) and accuracy percentage as you type
- **Quote-based Challenges**: Practice with quotes fetched from an external API
- **Sleek Dark Mode UI**: Enjoy a modern, eye-friendly interface with monospace font
- **Responsive Design**: Use on desktop or mobile devices with a consistent experience
- **Automatic Test Completion**: Test automatically stops when you reach the end of the quote
- **One-click Reset**: Easily start a new test with the "New Quote" button

## 🏗️ Project Structure

```
type-master/
├── src/
│   ├── components/
│   │   └── TypeTest.vue
│   ├── App.vue
│   ├── style.css
│   └── main.ts
├── public/
│   └── typewriter.png
├── package.json
├── tsconfig.json
└── README.md
```

## 🚦 Getting Started

### Prerequisites

- Node.js (version 14.x or higher)
- (p)npm or yarn

### Installation

1. Clone the repository
   ```
   git clone https://github.com/cseri502/type-master.git
   ```

2. Navigate to the project directory
   ```
   cd type-master
   ```

3. Install dependencies
   ```
   (p)npm install
   # or
   yarn install
   ```

4. Start the development server
   ```
   (p)npm run dev
   # or
   yarn dev
   ```

5. Open your browser and visit `http://localhost:5173`

## 🔧 Configuration

You can modify the difficulty levels by adjusting the length parameters in the `difficulties` object:

```typescript
const difficulties = {
    easy: { minLength: 50, maxLength: 100 },
    medium: { minLength: 100, maxLength: 200 },
    hard: { minLength: 200, maxLength: 300 }
};
```

## ⏩ References
- <a href="https://www.flaticon.com/free-icons/type" title="type icons">Type icons created by Freepik - Flaticon</a>

➡️ [Check out my other projects](https://github.com/cseri502)