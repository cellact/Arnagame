# 🐍 Arnagame - Classic Snake Game

A modern, responsive implementation of the classic Snake Game built with HTML5, CSS3, and JavaScript. Play it live on GitHub Pages!

## 🚀 [Play the Game](https://yourusername.github.io/Arnagame/)

## 🎮 Features

- **Classic Gameplay**: Navigate the snake to eat food and grow longer
- **Modern UI**: Sleek design with neon green aesthetics and smooth animations
- **Responsive Design**: Works perfectly on desktop and mobile devices
- **Touch Controls**: Mobile-friendly touch buttons for easy gameplay
- **Keyboard Controls**: Arrow keys for movement, spacebar to pause
- **Score Tracking**: Keep track of your high score
- **Game States**: Pause/resume functionality and game over screen

## 🕹️ How to Play

### Desktop Controls
- **Arrow Keys**: Move the snake (Up, Down, Left, Right)
- **Spacebar**: Pause/Resume the game

### Mobile Controls
- Use the on-screen directional buttons
- Tap the pause button (⏸) to pause/resume

### Rules
- Eat the red food to grow and increase your score
- Avoid hitting the walls or your own body
- The game gets more challenging as your snake grows longer

## 🛠️ Local Development

1. **Clone the repository:**
   ```bash
   git clone https://github.com/yourusername/Arnagame.git
   cd Arnagame
   ```

2. **Open the game:**
   Simply open `index.html` in your web browser, or use a local server:
   ```bash
   # Using Python 3
   python -m http.server 8000
   
   # Using Node.js (if you have http-server installed)
   npx http-server
   ```

3. **Visit:** `http://localhost:8000`

## 🚀 Deployment

This project is configured for automatic deployment to GitHub Pages using GitHub Actions.

### Automatic Deployment
- Every push to the `main` branch automatically deploys to GitHub Pages
- The deployment workflow is defined in `.github/workflows/deploy.yml`

### Manual Setup (if needed)
1. Go to your repository settings
2. Navigate to "Pages" in the sidebar
3. Set source to "GitHub Actions"
4. The site will be available at `https://yourusername.github.io/Arnagame/`

## 📁 Project Structure

```
Arnagame/
├── index.html                 # Main game file (HTML, CSS, JS all-in-one)
├── .github/
│   └── workflows/
│       └── deploy.yml         # GitHub Pages deployment workflow
└── README.md                  # This file
```

## 🎨 Technical Details

### Technologies Used
- **HTML5 Canvas**: For game rendering
- **CSS3**: Modern styling with gradients and animations
- **Vanilla JavaScript**: Game logic and interactivity
- **GitHub Actions**: Automated deployment

### Game Features
- **Grid-based Movement**: 20x20 pixel grid system
- **Collision Detection**: Wall and self-collision detection
- **Responsive Canvas**: Adapts to different screen sizes
- **Performance Optimized**: Smooth 60 FPS gameplay

### Browser Compatibility
- Modern browsers (Chrome, Firefox, Safari, Edge)
- Mobile browsers (iOS Safari, Chrome Mobile)
- Requires JavaScript enabled

## 🔧 Customization

You can easily customize the game by modifying the variables in `index.html`:

```javascript
// Game speed (lower = faster)
setTimeout(gameLoop, 200);

// Grid size
const gridSize = 20;

// Colors
const snakeColor = '#00ff00';  // Snake color
const foodColor = '#ff0000';   // Food color
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature-name`
3. Commit your changes: `git commit -am 'Add some feature'`
4. Push to the branch: `git push origin feature-name`
5. Submit a pull request

## 📝 License

This project is open source and available under the [MIT License](LICENSE).

## 🎯 Future Enhancements

- [ ] High score persistence using localStorage
- [ ] Multiple difficulty levels
- [ ] Power-ups and special food items
- [ ] Sound effects and background music
- [ ] Multiplayer mode
- [ ] Custom themes and skins

## 📞 Support

If you encounter any issues or have questions, please [open an issue](https://github.com/yourusername/Arnagame/issues) on GitHub.

---

Made with ❤️ and JavaScript | [Live Demo](https://yourusername.github.io/Arnagame/)
