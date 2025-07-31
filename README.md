
# Dogecoin Dash 🐶💸

[![Grok Challenge](https://img.shields.io/badge/Grok-Challenge-%23GrokChallenge-blue)](https://x.com/hashtag/GrokChallenge)  
[![Play Now](https://img.shields.io/badge/Play-Web-brightgreen)](https://username.github.io/DogecoinDash)  
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Welcome to **Dogecoin Dash**, an 8-bit-style, chiptune-fueled endless runner built with Flutter and Flame for the **Grok Challenge**! 🚀 Powered by Grok (xAI), this game features a Shiba Inu dashing across Mars to collect Dogecoins, with **Dogecoin King** (Tesla-mantled, Elon-inspired) sprinkling bonus coins and **Ani-chan** (pro artist’s 8-bit-style monochrome goth-loli with blonde twin-tails, 320x96) laying down with a "DOON!" in the bonus stage. Play instantly on itch.io/Game Jolt, follow live development on GitHub, and join #GrokChallenge on X to make it viral! 😎

> **Play now**: [itch.io](#) | [Game Jolt](#) | **Follow**: [#GrokChallenge](https://x.com/hashtag/GrokChallenge) | **Contribute**: [GitHub Issues](#)

---

## 🎮 Game Concept

**Dogecoin Dash** is a fast, offline, 8-bit-style endless runner where a Shiba Inu sprints across a tiled Mars landscape (256x96) to collect Dogecoins. Choose skins with unique traits, dodge Martian rocks (losing 10 coins per hit), and unlock the bonus stage with **Ani-chan** (320x96, goth-loli). Run past her for extra points, with Mars' low gravity enabling adjustable jumps based on button press duration! Built with Grok’s code and pro pixel art, live on GitHub.

- **Genre**: 2D Endless Runner
- **Platform**: Web (Flutter Web, mobile/PC via itch.io/Game Jolt)
- **Screen Size**: 256x96 pixels (scaled up, e.g., 1024x384 for Web)
- **Target Audience**: Indie gamers, Dogecoin fans, art enthusiasts, Elon Musk 😜
- **Tone**: Chiptune, 8-bit-style, meme-heavy with Dogecoin/Tesla vibes
- **Art Style**: 8-bit-style pixel art (monochrome, 4-color gray palette)

---

## ✨ Detailed Specifications

### 1. Sprite Specifications
All sprites use a 4-color gray palette (black, white, light gray, dark gray).

- **Player Characters (Skins)**:
  - **Default Shiba**: 16x16 pixels, speed (-100 to 100 pixels/second), jump (0-48 pixels, 0.0-0.5 seconds press), free.
  - **Tesla Shiba**: 16x16 pixels, 1.5x speed (-150 to 150 pixels/second), jump (0-57 pixels, 0.0-0.5 seconds press), 1 durability (ignores 1 hit/stage), $0.99 IAP.
  - **Ani-chan**: 24x24 pixels, speed (-100 to 100 pixels/second), jump (0-48 pixels, 0.0-0.5 seconds press), larger hitbox, 2x bonus stage score (+1000 points), $1.99 IAP.
  - **Animation**: 0.2 seconds/frame, 4-frame loop.
  - **Jump**: Mars low gravity, height adjustable by button press (max 48 or 57 pixels), 1.0-second total duration.

- **NPC: Dogecoin King**:
  - **Size**: 24x24 pixels, 4-color gray + Tesla logo accent.
  - **Design**: Crown, sunglasses, Tesla mantle, 10% spawn chance.
  - **Animation**: Coin sprinkle (4 frames, 0.2 seconds/frame).

- **Obstacles: Martian Rocks**:
  - **Size**: 16x16 pixels, 4-color gray.
  - **Design**: Angular rocks (Kenney.nl-based, monochrome), random spawn (5-10 seconds).
  - **Effect**: 2-frame shake (0.1 seconds) on collision, -10 coins penalty.

- **Collectibles: Dogecoin**:
  - **Size**: 16x16 pixels, 4-color gray.
  - **Design**: Simple coin (Kenney.nl-based, monochrome), sparkle effect.
  - **Animation**: Blink (4 frames, 0.2 seconds/frame), +100 points.

- **Effects: Stars**:
  - **Size**: 8x8 pixels, 4-color gray.
  - **Design**: 4-pixel glow, random placement.
  - **Animation**: Blink (4 frames, 0.3 seconds/frame).

- **Tools**: Aseprite (or LibreSprite); Procreate/Photoshop for sketches, pixelized in Aseprite.

### 2. Background Specifications
- **Mars Landscape**:
  - **Size**: 256x64 (ground) + 256x32 (sky) = 256x96 pixels, 4-color gray.
  - **Design**: Seamless tiled ground (rocks, craters) + starry sky, 8-bit-style.
  - **Tiling**: `ParallaxComponent`, ground (-50 pixels/second), sky (-25 pixels/second).
- **Bonus Stage**:
  - **Size**: 320x96 pixels (Ani-chan, 4-color gray).
  - **Design**: Goth-loli Ani-chan (blonde twin-tails, frill dress) laying down, overlaid on Mars ground.
  - **Movement**: `ParallaxComponent`, -100 pixels/second, 10-second duration.
  - **Effects**: Stars (8x8), coins (16x16) with blink animations.

- **Sample Code**:
  ```dart
  import 'package:flame/components.dart';
  import 'package:flame/parallax.dart';

  class MarsBackground extends ParallaxComponent {
    @override
    Future<void> onLoad() async {
      parallax = await gameRef.loadParallax([
        ParallaxImageData('mars_ground_mono.png', repeat: ParallaxRepeat.repeatX, velocityMultiplier: Vector2(1, 0)),
        ParallaxImageData('mars_sky_mono.png', repeat: ParallaxRepeat.repeatX, velocityMultiplier: Vector2(0.5, 0)),
      ], baseVelocity: Vector2(-50, 0));
    }
  }

  class BonusStage extends ParallaxComponent {
    @override
    Future<void> onLoad() async {
      parallax = await gameRef.loadParallax([
        ParallaxImageData('mars_ground_mono.png', repeat: ParallaxRepeat.repeatX, velocityMultiplier: Vector2(1, 0)),
        ParallaxImageData('ani_laying_mono_gothloli.png', repeat: ParallaxRepeat.none, velocityMultiplier: Vector2(2, 0)),
      ], baseVelocity: Vector2(-100, 0));
      for (int i = 0; i < 5; i++) {
        add(SpriteAnimationComponent(
          animation: await gameRef.loadSpriteAnimation('coin_mono_sparkle.png', SpriteAnimationData.sequenced(amount: 4, stepTime: 0.2, textureSize: Vector2.all(16))),
          position: Vector2(50 + i * 30, 20),
        ));
      }
      Future.delayed(Duration(seconds: 10), () => gameRef.endBonusStage());
    }
  }
```
---

## 3. Gameplay Specifications

- Triggers: Bonus stage after 1000 coins or 10 minutes, lasts 10 seconds.
- Movement:
    - Player: Left-right (speed varies by skin), jump (0-48 or 57 pixels, 1.0-second duration).
    - Obstacles/Coins: -50 pixels/second, random spawn (5-10 seconds/3-5 seconds).
- Scoring: Coin (+100 points), bonus stage completion (+500 or +1000 with Ani-chan).
- Game Over: 3 hits (Tesla Shiba ignores 1 hit).
- Collision Penalty: -10 coins per rock hit, clamped at 0.

## 4. UI Specifications

- Coin Display:
    - Position: Bottom-right (x=220, y=80 on 256x96 screen).
    - Design: 16x16 coin icon + 8-bit-style text (4x8 pixels).
    - Function: Shows collected coins, updates on collect/lose.

## 5. Monetization

- AdMob: Banner (bottom), interstitial (post-game over).
- IAP: Tesla Shiba ($0.99), Ani-chan ($1.99), King Boost ($0.99).
- Dogecoin Tipping: QR code on game-over screen.

## 6. Sound

- Music: Pixabay 8-bit chiptune.
- Effects: Jump, collision ("piro-piro"), coin collect ("chin!"), land ("thud").

---

## 🛠️ Development Plan
 
 Built with Flutter and Flame. Grok assists with code and ideas. Live on GitHub.Tech Stack

- Framework: Flutter + Flame
- Assets: Custom Ani-chan (320x96), free assets (Kenney.nl)
- Deployment: itch.io, Game Jolt, GitHub Pages
- Monetization: AdMob, IAP, Dogecoin tipping
- Tools: Aseprite, VS Code, Filmora, Grok

### Milestones

**1. Prototype (1 Week):**
    - Shiba (16x16), rocks (16x16), coins (16x16), coin display, adjustable Mars jump.
    - Ani-chan (320x96) refinement.
    - Grok: "Jump with button press code".
**2. Alpha (2 Weeks):**
    - Dogecoin King (24x24), bonus stage.
    - AdMob integration.
    - itch.io/Game Jolt launch.
**3. Release (3 Weeks):**
    - Skins, IAP, tipping.
    - Audio, trailer.
    - X campaign.

---

## 📣 Viral Strategy (#GrokChallenge)

- 10-Second Trailer: Shiba, Ani-chan (320x96), King. Text: "Grok’s Dogecoin Dash! Adjustable Mars jumps! [itch.io link] #GrokChallenge"
- Real-Time Dev: "Mars jump by press duration added! [GitHub link] #DogecoinDash"
- Community: Polls, Reddit posts.
- Elon Bait: "@elonmusk, goth-loli Ani’s DOON! on Mars jumps! [itch.io link] #GrokChallenge"

---

## 💰 Monetization

- AdMob: $50-300/month at 10K plays.
- IAP: Skins ($0.99-$2.99), ad removal ($1.99).
- Dogecoin Tipping: $10-100 at 10K plays.
- itch.io/Game Jolt: PWYW, ads.

---

## 🚀 Why Dogecoin Dash?

- Goth-loli Art: Pro artist’s Ani-chan!
- Mars Gravity: Adjustable jumps for strategy!
- Grok-Powered: AI-driven, GitHub live.
- Meme Appeal: Shiba + Ani-chan + Tesla King.
- Community-Driven: X/GitHub ideas.
- Fast & Free: Web play.

---

## 🐾 Join the Challenge!

1. Play: itch.io (#) | Game Jolt (#)
2. Contribute: GitHub Issues (#)
3. Share: #GrokChallenge #DogecoinDash!
4. Tip: Send Dogecoin! QR Code (#)
5. Follow: [#GrokChallenge](/hashtag/GrokChallenge)

Conquer Mars with goth-loli Ani-chan’s DOON!@elonmusk, King? 😎

---
 
 📜 LicenseMIT License.

---
Created with ❤️, Grok, and pro artist’s goth-loli Ani-chan by [izumix77]. Powered by xAI.
