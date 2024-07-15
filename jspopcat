// Create the GUI
const guiContainer = document.createElement('div');
guiContainer.style.position = 'fixed';
guiContainer.style.top = '10px';
guiContainer.style.right = '10px';
guiContainer.style.padding = '10px';
guiContainer.style.backgroundColor = 'rgba(0, 0, 0, 0.7)';
guiContainer.style.color = 'white';
guiContainer.style.zIndex = 10000;
guiContainer.style.borderRadius = '5px';
guiContainer.style.cursor = 'move';
guiContainer.style.userSelect = 'none';
guiContainer.style.transition = 'transform 0.2s';
document.body.appendChild(guiContainer);

// Add a title
const title = document.createElement('h3');
title.innerText = 'Auto Clicker';
title.style.margin = '0 0 10px 0';
title.style.cursor = 'move';
guiContainer.appendChild(title);

// Add a start button
const startButton = document.createElement('button');
startButton.innerText = 'Start';
startButton.style.marginRight = '10px';
startButton.style.padding = '5px 10px';
startButton.style.cursor = 'pointer';
guiContainer.appendChild(startButton);

// Add a stop button
const stopButton = document.createElement('button');
stopButton.innerText = 'Stop';
stopButton.style.padding = '5px 10px';
stopButton.style.cursor = 'pointer';
guiContainer.appendChild(stopButton);

// Add interval input
const intervalLabel = document.createElement('label');
intervalLabel.innerText = 'Interval (ms): ';
intervalLabel.style.marginLeft = '10px';
guiContainer.appendChild(intervalLabel);

const intervalInput = document.createElement('input');
intervalInput.type = 'number';
intervalInput.value = localStorage.getItem('interval') || 50;
intervalInput.style.width = '60px';
intervalInput.style.marginLeft = '5px';
intervalInput.style.padding = '5px';
guiContainer.appendChild(intervalInput);

// Add pop count input
const popCountLabel = document.createElement('label');
popCountLabel.innerText = 'Total Pops: ';
popCountLabel.style.marginLeft = '10px';
guiContainer.appendChild(popCountLabel);

const popCountInput = document.createElement('input');
popCountInput.type = 'number';
popCountInput.value = localStorage.getItem('totalPops') || 100;
popCountInput.style.width = '60px';
popCountInput.style.marginLeft = '5px';
popCountInput.style.padding = '5px';
guiContainer.appendChild(popCountInput);

// Add click count display
const clickCountLabel = document.createElement('p');
clickCountLabel.innerText = `Clicks: ${localStorage.getItem('clickCount') || 0}`;
clickCountLabel.style.marginTop = '10px';
guiContainer.appendChild(clickCountLabel);

// Add funny quote display
const quoteLabel = document.createElement('p');
quoteLabel.innerText = 'Ready to pop!';
quoteLabel.style.marginTop = '10px';
quoteLabel.style.fontStyle = 'italic';
guiContainer.appendChild(quoteLabel);

// Auto clicker function
let autoClickerInterval;
let clickCount = parseInt(localStorage.getItem('clickCount')) || 0;
const autoClicker = () => {
  document.dispatchEvent(new KeyboardEvent('keydown', {'key': 'g'}));
  clickCount++;
  clickCountLabel.innerText = `Clicks: ${clickCount}`;
  localStorage.setItem('clickCount', clickCount);
  guiContainer.style.transform = `rotate(${clickCount % 20 - 10}deg)`; // Funny shake animation
};

// Funny quotes
const quotes = [
  "Pop 'til you drop!",
  "Pop, pop, pop!",
  "Keep on popping!",
  "Pop mania!",
  "Can't stop the pop!",
  "Poppity pop pop!"
];

const getRandomQuote = () => quotes[Math.floor(Math.random() * quotes.length)];

// Play sound effect
const popSound = new Audio('https://www.myinstants.com/media/sounds/popcat.mp3');

// Start auto clicker
startButton.addEventListener('click', () => {
  if (!autoClickerInterval) {
    const interval = parseInt(intervalInput.value);
    const totalPops = parseInt(popCountInput.value);
    localStorage.setItem('interval', interval);
    localStorage.setItem('totalPops', totalPops);

    autoClickerInterval = setInterval(() => {
      if (clickCount < totalPops) {
        autoClicker();
        popSound.play();
        quoteLabel.innerText = getRandomQuote();
      } else {
        clearInterval(autoClickerInterval);
        autoClickerInterval = null;
        guiContainer.style.transform = 'rotate(0deg)'; // Reset rotation
        alert("You've reached the set number of pops!");
      }
    }, interval);
  }
});

// Stop auto clicker
stopButton.addEventListener('click', () => {
  clearInterval(autoClickerInterval);
  autoClickerInterval = null;
  guiContainer.style.transform = 'rotate(0deg)'; // Reset rotation
});

// Make the GUI draggable
let isDragging = false;
let offsetX, offsetY;

guiContainer.addEventListener('mousedown', (e) => {
  if (e.target !== startButton && e.target !== stopButton && e.target !== intervalInput && e.target !== popCountInput) {
    isDragging = true;
    offsetX = e.clientX - guiContainer.getBoundingClientRect().left;
    offsetY = e.clientY - guiContainer.getBoundingClientRect().top;
  }
});

document.addEventListener('mousemove', (e) => {
  if (isDragging) {
    guiContainer.style.left = `${e.clientX - offsetX}px`;
    guiContainer.style.top = `${e.clientY - offsetY}px`;
    guiContainer.style.right = 'auto';
  }
});

document.addEventListener('mouseup', () => {
  isDragging = false;
});
