# Dogecoin Dash 🐶💸

[![Grok Challenge](https://img.shields.io/badge/Grok-Challenge-%23GrokChallenge-blue)](/hashtag/GrokChallenge)  
[![Play Now](https://img.shields.io/badge/Play-Web-brightgreen)](https://username.github.io/DogecoinDash)  
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)Welcome to Dogecoin Dash, an 8-bit-style, chiptune-powered endless runner built with Godot for the Grok Challenge! 🚀 Powered by Grok (xAI), it stars a Shiba Inu sprinting across Mars to collect Dogecoins, with Dogecoin King (Tesla-mantled, Elon-inspired) sprinkling bonus coins and Ani-chan (pro artist’s monochrome goth-loli with blonde twin-tails, 320x96) dropping a “DOON!” in the bonus stage. Play instantly on itch.io/Game Jolt, follow live development on GitHub, and join #GrokChallenge on X to make it viral! 😎

Play: itch.io (#) | Game Jolt (#)  
Follow: [#GrokChallenge](/hashtag/GrokChallenge)  
Contribute: GitHub Issues (#)

---

## 🎮 Game Concept
 Dogecoin Dash is a fast-paced, offline, 8-bit-style endless runner where a Shiba Inu dashes across a tiled 256x96 Mars landscape to collect Dogecoins. Choose skins with unique traits, dodge Martian rocks (-10 coins per hit), and unlock a bonus stage with Ani-chan (320x96, goth-loli). Master Mars’ low gravity with adjustable jumps based on button press duration! Built with Grok’s code and pro pixel art, live on GitHub.

- Genre: 2D Endless Runner
- Platform: Web (Godot HTML5 export), Mobile/PC (itch.io/Game Jolt)
- Screen Size: 256x96 pixels (scaled, e.g., 1024x384 for Web)
- Target Audience: Indie gamers, Dogecoin fans, art enthusiasts, Elon Musk 😜
- Tone: Chiptune, 8-bit, meme-heavy with Dogecoin/Tesla vibes
- Art Style: 8-bit pixel art (4-color gray palette: black, white, light gray, dark gray)

---

## ✨ Detailed Specifications
 
 1. Sprite SpecificationsAll sprites use a 4-color gray palette (black, white, light gray, dark gray).

- Player Characters (Skins):
    - Default Shiba: 16x16 pixels, speed (-100 to 100 pixels/second), jump (0-48 pixels, 0.0-0.5s press), free.
    - Tesla Shiba: 16x16 pixels, 1.5x speed (-150 to 150 pixels/second), jump (0-57 pixels, 0.0-0.5s press), 1 durability (ignores 1 hit/stage), $0.99 IAP.
    - Ani-chan: 24x24 pixels, speed (-100 to 100 pixels/second), jump (0-48 pixels, 0.0-0.5s press), larger hitbox, 2x bonus stage score (+1000 points), $1.99 IAP.
    - Animation: 0.2s/frame, 4-frame loop.
    - Jump: Mars low gravity, height adjustable by button press (max 48/57 pixels), 1s duration.
- NPC: Dogecoin King:
    - Size: 24x24 pixels, 4-color gray + Tesla logo accent.
    - Design: Crown, sunglasses, Tesla mantle, 10% spawn chance.
    - Animation: Coin sprinkle (4 frames, 0.2s/frame).
- Obstacles: Martian Rocks:
    - Size: 16x16 pixels, 4-color gray.
    - Design: Angular rocks (Kenney.nl-based, monochrome), random spawn (5-10s).
    - Effect: 2-frame shake (0.1s) on collision, -10 coins penalty.
- Collectibles: Dogecoin:
    - Size: 16x16 pixels, 4-color gray.
    - Design: Simple coin (Kenney.nl-based, monochrome), sparkle effect.
    - Animation: Blink (4 frames, 0.2s/frame), +100 points.
- Effects: Stars:
    - Size: 8x8 pixels, 4-color gray.
    - Design: 4-pixel glow, random placement.
    - Animation: Blink (4 frames, 0.3s/frame).
- Tools: Aseprite (or LibreSprite); Procreate/Photoshop for sketches, pixelized in Aseprite.

2. Background Specifications

- Mars Landscape:
    - Size: 256x64 (ground) + 256x32 (sky) = 256x96 pixels, 4-color gray.
    - Design: Seamless tiled ground (rocks, craters) + starry sky, 8-bit style.
    - Parallax: ParallaxBackground, ground (-50 pixels/second), sky (-25 pixels/second).
- Bonus Stage:
    - Size: 320x96 pixels (Ani-chan, 4-color gray).
    - Design: Goth-loli Ani-chan (blonde twin-tails, frill dress, lying down), overlaid on Mars ground.
    - Movement: ParallaxLayer, -100 pixels/second, 10s duration.
    - Effects: Stars (8x8), coins (16x16) with blink animations.
- Sample Code:
    
    gdscript
    
    ```gdscript
    extends ParallaxBackground
    
    func _ready():
        $GroundLayer.motion_offset.x = -50
        $SkyLayer.motion_offset.x = -25
    
    func _physics_process(delta):
        scroll_offset.x -= 50 * delta
    ```
    

3. Gameplay Specifications

- Triggers: Bonus stage after 1000 coins or 10 minutes, lasts 10s.
- Movement:
    - Player: Left-right (speed varies by skin), jump (0-48/57 pixels, 1s duration).
    - Obstacles/Coins: -50 pixels/second, random spawn (rocks: 5-10s, coins: 3-5s).
- Scoring: Coin (+100 points), bonus stage completion (+500 or +1000 with Ani-chan).
- Game Over: 3 hits (Tesla Shiba ignores 1 hit).
- Collision Penalty: -10 coins per rock hit, clamped at 0.

4. UI Specifications

- Coin Display:
    - Position: Bottom-right (x=220, y=80 on 256x96 screen).
    - Design: 16x16 coin icon + 8-bit text (4x8 pixels).
    - Function: Updates on coin collect/loss.

5. Monetization

- AdMob: Banner (bottom), interstitial (post-game over).
- IAP: Tesla Shiba ($0.99), Ani-chan ($1.99), King Boost ($0.99).
- Dogecoin Tipping: QR code on game-over screen.

6. Sound

- Music: Pixabay 8-bit chiptune, looped.
- Effects: Jump (“piro-piro”), collision (“chin!”), land (“thud”).

---

## 🛠️ Development Plan

 Built with Godot and GDScript, leveraging Grok’s code assistance, live on GitHub.

- Tech Stack:
    - Engine: Godot (GDScript)
    - Assets: Custom Ani-chan (320x96), free assets (Kenney.nl)
    - Deployment: itch.io, Game Jolt, HTML5 export
    - Monetization: AdMob (plugin), IAP, Dogecoin tipping
    - Tools: Aseprite, Godot Editor, Filmora, Grok
- Milestones:
    1. Prototype (1 Week): Shiba (16x16), rocks, coins, coin display, Mars jump.
    2. Alpha (2 Weeks): Dogecoin King, bonus stage, AdMob integration, itch.io/Game Jolt launch.
    3. Release (3 Weeks): Skins, IAP, chiptune, trailer, X campaign.

---

## 📣 Viral Strategy (#GrokChallenge)

- 10-Second Trailer: Shiba, Ani-chan (320x96), King. Text: “Grok’s Dogecoin Dash! Mars jumps! [itch.io link] #GrokChallenge”
- Real-Time Dev: “Mars jump by press duration added! [GitHub link] #DogecoinDash”
- Community: Polls, Reddit posts.
- Elon Bait: “
    
    @elonmusk
    
    , goth-loli Ani’s DOON! on Mars jumps! [itch.io link] #GrokChallenge”

---

## 💰 Monetization

- AdMob: $50-300/month at 10K plays.
- IAP: Skins ($0.99-$2.99), ad removal ($1.99).
- Dogecoin Tipping: $10-100 at 10K plays.
- itch.io/Game Jolt: PWYW (Pay What You Want), ads.

---

## 🚀 Why Dogecoin Dash?

- Goth-loli Art: Pro artist’s Ani-chan!
- Mars Gravity: Strategic adjustable jumps!
- Grok-Powered: AI-driven, GitHub live.
- Meme Appeal: Shiba + Ani-chan + Tesla King.
- Community-Driven: X/GitHub ideas.
- Fast & Free: Web play.

---

## 🐾 Join the Challenge!

1. Play: itch.io (#) | Game Jolt (#)
2. Contribute: GitHub Issues (#)
3. Share: #GrokChallenge #DogecoinDash
4. Tip: Send Dogecoin! QR Code (#)
5. Follow: #GrokChallenge (/hashtag/GrokChallenge)

Conquer Mars with goth-loli Ani-chan’s DOON!@elonmusk, King? 😎 

---

 📜 LicenseMIT License

---

Created with ❤️, Grok, and pro artist’s goth-loli Ani-chan by [izumix77]. Powered by xAI.
