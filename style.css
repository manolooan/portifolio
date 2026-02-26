const openLetterBtn = document.getElementById("openLetterBtn");
const letterCard = document.getElementById("letterCard");
const typingText = document.getElementById("typingText");
const toggleMusicBtn = document.getElementById("toggleMusicBtn");
const bgMusic = document.getElementById("bgMusic");

const daysEl = document.getElementById("days");
const hoursEl = document.getElementById("hours");
const minutesEl = document.getElementById("minutes");
const secondsEl = document.getElementById("seconds");

const scoreEl = document.getElementById("score");
const spawnHeartBtn = document.getElementById("spawnHeartBtn");
const gameArea = document.getElementById("gameArea");
const unlockMessage = document.getElementById("unlockMessage");

const slides = Array.from(document.querySelectorAll(".slide"));
const prevSlide = document.getElementById("prevSlide");
const nextSlide = document.getElementById("nextSlide");
const currentYear = document.getElementById("currentYear");

let typingIndex = 0;
let typingTimer;
let isMusicPlaying = false;
let score = 0;
let gameInterval;
let currentSlideIndex = 0;

function typeLetterMessage() {
  const message = typingText.dataset.message || "";
  typingText.textContent = "";
  clearInterval(typingTimer);
  typingIndex = 0;

  typingTimer = setInterval(() => {
    typingText.textContent += message.charAt(typingIndex);
    typingIndex += 1;

    if (typingIndex >= message.length) {
      clearInterval(typingTimer);
    }
  }, 28);
}

openLetterBtn.addEventListener("click", () => {
  letterCard.classList.remove("hidden");
  letterCard.animate(
    [
      { opacity: 0, transform: "translateY(16px)" },
      { opacity: 1, transform: "translateY(0)" }
    ],
    { duration: 520, easing: "ease-out" }
  );

  typeLetterMessage();
  document.getElementById("carta").scrollIntoView({ behavior: "smooth", block: "center" });
});

toggleMusicBtn.addEventListener("click", async () => {
  if (!isMusicPlaying) {
    try {
      await bgMusic.play();
      isMusicPlaying = true;
      toggleMusicBtn.textContent = "Pausar música ⏸️";
    } catch (error) {
      toggleMusicBtn.textContent = "Toque para permitir música 🎵";
    }
  } else {
    bgMusic.pause();
    isMusicPlaying = false;
    toggleMusicBtn.textContent = "Tocar música 🎵";
  }
});

function updateCountdown() {
  const targetDate = new Date("2027-02-26T00:00:00");
  const now = new Date();
  const diff = targetDate - now;

  if (diff <= 0) {
    daysEl.textContent = "00";
    hoursEl.textContent = "00";
    minutesEl.textContent = "00";
    secondsEl.textContent = "00";
    return;
  }

  const day = Math.floor(diff / (1000 * 60 * 60 * 24));
  const hour = Math.floor((diff / (1000 * 60 * 60)) % 24);
  const minute = Math.floor((diff / (1000 * 60)) % 60);
  const second = Math.floor((diff / 1000) % 60);

  daysEl.textContent = String(day).padStart(2, "0");
  hoursEl.textContent = String(hour).padStart(2, "0");
  minutesEl.textContent = String(minute).padStart(2, "0");
  secondsEl.textContent = String(second).padStart(2, "0");
}

function createHeart() {
  const heart = document.createElement("span");
  heart.className = "heart";
  heart.textContent = "💚";

  const x = Math.random() * (gameArea.clientWidth - 32);
  const y = Math.random() * (gameArea.clientHeight - 32);

  heart.style.left = `${x}px`;
  heart.style.top = `${y}px`;

  heart.addEventListener("click", () => {
    score += 1;
    scoreEl.textContent = String(score);
    heart.remove();

    if (score >= 10) {
      unlockMessage.classList.remove("hidden");
      burstHearts();
      clearInterval(gameInterval);
      spawnHeartBtn.textContent = "Jogar de novo";
    }
  });

  gameArea.appendChild(heart);

  setTimeout(() => {
    heart.remove();
  }, 1700);
}

function burstHearts() {
  for (let i = 0; i < 14; i += 1) {
    const burst = document.createElement("span");
    burst.className = "heart";
    burst.textContent = i % 2 === 0 ? "💚" : "💖";
    burst.style.left = `${Math.random() * (gameArea.clientWidth - 32)}px`;
    burst.style.top = `${Math.random() * (gameArea.clientHeight - 32)}px`;
    gameArea.appendChild(burst);

    setTimeout(() => burst.remove(), 1400);
  }
}

spawnHeartBtn.addEventListener("click", () => {
  score = 0;
  scoreEl.textContent = "0";
  unlockMessage.classList.add("hidden");
  clearInterval(gameInterval);
  gameArea.innerHTML = "";

  createHeart();
  gameInterval = setInterval(createHeart, 820);
  spawnHeartBtn.textContent = "Em andamento...";
});

function showSlide(index) {
  slides.forEach((slide, slideIndex) => {
    slide.classList.toggle("active", slideIndex === index);
  });
}

nextSlide.addEventListener("click", () => {
  currentSlideIndex = (currentSlideIndex + 1) % slides.length;
  showSlide(currentSlideIndex);
});

prevSlide.addEventListener("click", () => {
  currentSlideIndex = (currentSlideIndex - 1 + slides.length) % slides.length;
  showSlide(currentSlideIndex);
});

let touchStartX = 0;
let touchEndX = 0;

const carousel = document.getElementById("carousel");
carousel.addEventListener("touchstart", (event) => {
  touchStartX = event.changedTouches[0].screenX;
});

carousel.addEventListener("touchend", (event) => {
  touchEndX = event.changedTouches[0].screenX;
  const distance = touchEndX - touchStartX;

  if (distance < -40) {
    nextSlide.click();
  } else if (distance > 40) {
    prevSlide.click();
  }
});

const revealElements = document.querySelectorAll(".reveal");
const observer = new IntersectionObserver(
  (entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        entry.target.classList.add("visible");
      }
    });
  },
  { threshold: 0.15 }
);

revealElements.forEach((element) => observer.observe(element));

currentYear.textContent = String(new Date().getFullYear());
updateCountdown();
setInterval(updateCountdown, 1000);
