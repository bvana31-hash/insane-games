#// InsaniGames.com - World's Craziest Games Website
import React, { useEffect, useRef, useState } from "react";
import { Flame, Sparkles, Laugh, Gamepad2, Ghost } from "lucide-react";

// Background music file (place in /public/sounds/crazy_theme.mp3)
const bgMusicUrl = "/sounds/crazy_theme.mp3";

// Example games (you can add up to 50)
const games = [
  {
    title: "Super Pooper",
    category: "Meme-Lord Games",
    description: "A chaotic toilet simulator where everything goes wrong.",
  },
  {
    title: "Banana Rampage",
    category: "Insane & Chaotic",
    description: "Throw bananas at literally everything until the world breaks.",
  },
  {
    title: "Ghost Puncher",
    category: "Absurd",
    description: "Punch invisible ghosts before they punch you.",
  },
];

const categories = [
  { icon: <Flame />, name: "Cool & Crazy" },
  { icon: <Sparkles />, name: "Experimental" },
  { icon: <Laugh />, name: "Meme-Lord Games" },
  { icon: <Gamepad2 />, name: "Insane & Chaotic" },
  { icon: <Ghost />, name: "Absurd" },
];

export default function InsaniGames() {
  const audioRef = useRef(null);
  const [playing, setPlaying] = useState(null); // which game is being played

  useEffect(() => {
    if (audioRef.current) {
      audioRef.current.volume = 0.3;
      audioRef.current.play().catch(() => {});
    }
  }, []);

  return (
    <div className="bg-black text-white min-h-screen p-4 relative overflow-x-hidden">
      {/* Background Music */}
      <audio ref={audioRef} loop src={bgMusicUrl} />

      {/* Header */}
      <header className="text-center py-10 animate-bounce">
        <h1 className="text-5xl font-bold animate-pulse text-red-500">
          🎮 InsaniGames.com
        </h1>
        <p className="text-xl mt-2">50 of the World’s Craziest Games</p>
        <button className="mt-4 text-black bg-white hover:bg-gray-300 px-6 py-2 rounded-xl animate-wiggle">
          🎲 Take Me to Insanity
        </button>
      </header>

      {/* Categories */}
      <section className="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-5 gap-4 text-center py-4">
        {categories.map((cat, i) => (
          <div
            key={i}
            className="bg-gray-900 p-4 rounded-2xl shadow-md hover:bg-red-800 hover:scale-110 transition duration-300"
          >
            <div className="text-3xl mb-2">{cat.icon}</div>
            <div className="font-semibold text-lg">{cat.name}</div>
          </div>
        ))}
      </section>

      {/* Games */}
      <section className="py-6 grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6">
        {games.map((game, i) => (
          <div
            key={i}
            className="bg-gray-800 text-white rounded-2xl shadow-xl hover:shadow-red-500 hover:scale-105 transition duration-300 p-4"
          >
            <h2 className="text-xl font-bold text-red-400 mb-1">
              {game.title}
            </h2>
            <p className="text-sm italic text-gray-300 mb-2">
              {game.category}
            </p>
            <p className="text-sm text-gray-200 mb-2">{game.description}</p>

            {/* Load iframe only when clicked */}
            {playing === i ? (
              <iframe
                src={`/games/${game.title
                  .replaceAll(" ", "_")
                  .toLowerCase()}/index.html`}
                title={game.title}
                className="w-full h-48 border border-white mt-2"
                loading="lazy"
              ></iframe>
            ) : (
              <button
                onClick={() => setPlaying(i)}
                className="mt-4 w-full bg-white text-black hover:bg-red-200 px-4 py-2 rounded-lg"
              >
                ▶️ Play Now
              </button>
            )}
          </div>
        ))}
      </section>

      {/* Footer */}
      <footer className="text-center py-10 text-gray-400 animate-pulse">
        © 2025 InsaniGames. All rights melted.
      </footer>
    </div>
  );
}
