
# Dogecoin Dash 🐶💸

[![Grok Challenge](https://img.shields.io/badge/Grok-Challenge-%23GrokChallenge-blue)](https://x.com/hashtag/GrokChallenge)  
[![Play Now](https://img.shields.io/badge/Play-Web-brightgreen)](https://username.github.io/DogecoinDash)  
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Welcome to **Dogecoin Dash**, an 8-bit-style, chiptune-fueled endless runner built with Flutter and Flame for the **Grok Challenge**! 🚀 Powered by Grok (xAI), this game features a Shiba Inu dashing across Mars to collect Dogecoins, with **Dogecoin King** (Tesla-mantled, Elon-inspired) sprinkling bonus coins and **Ani-chan** (Grok’s mascot, a pro artist’s 8-bit-style monochrome goth-loli with blonde twin-tails, 320x64) laying down with a "DOON!" in the bonus stage. Play instantly on itch.io/Game Jolt, follow live development on GitHub, and join #GrokChallenge on X to make it viral! 😎

> **Play now**: [itch.io](#) | [Game Jolt](#) | **Follow**: [#GrokChallenge](https://x.com/hashtag/GrokChallenge) | **Contribute**: [GitHub Issues](#)

---

## 🎮 Game Concept

**Dogecoin Dash** is a fast, offline, 8-bit-style endless runner where a Shiba Inu sprints across a tiled Mars landscape to collect Dogecoins. Dodge Martian rocks, grab bonus coins from **Dogecoin King**, and unlock the bonus stage with a massive **Ani-chan** (pro artist’s 8-bit-style art, 320x64, blonde twin-tails, goth-loli fashion) laying across the screen. Run past her to end the stage. Built with Grok’s code and pro pixel art, live on GitHub.

- **Genre**: 2D Endless Runner
- **Platform**: Web (Flutter Web, mobile/PC via itch.io/Game Jolt)
- **Target Audience**: Indie gamers, Dogecoin fans, art enthusiasts, Elon Musk 😜
- **Tone**: Chiptune, 8-bit-style, meme-heavy with Dogecoin/Tesla vibes
- **Art Style**: 8-bit-style pixel art (monochrome, cheap, pro-artist flair)

---

## ✨ Detailed Specifications

### 1. Sprite Specifications
Sprites include player characters, NPCs, obstacles, collectibles, and effects, all in 8-bit-style monochrome (4-color gray palette: black, white, light gray, dark gray).

- **Player Characters (Skins)**:
  - **Default Shiba**: 16x16 pixels, 4-frame run animation (tail wag), free.
  - **Tesla Shiba**: 16x16 pixels, 4-frame run animation (mantle flutter), Tesla logo accent, $0.99 IAP.
  - **Ani-chan**: 24x24 pixels, 4-frame run animation (twin-tails sway + frill flutter), blonde twin-tails, goth-loli fashion, $1.99 IAP.
  - **Animation**: 0.2 seconds/frame, 4-frame loop for all skins.

- **NPC: Dogecoin King**:
  - **Size**: 24x24 pixels, 4-color gray + Tesla logo accent.
  - **Design**: Crown, sunglasses, Tesla-mantled Elon-inspired character, 10% spawn chance.
  - **Animation**: Coin sprinkle (4 frames, 0.2 seconds/frame).

- **Obstacles: Martian Rocks**:
  - **Size**: 16x16 pixels, 4-color gray.
  - **Design**: Angular rocks (based on Kenney.nl "Rocks", monochrome simplified), randomly spawned.
  - **Animation**: None, but 2-frame shake effect (0.1 seconds) on collision.

- **Collectibles: Dogecoin**:
  - **Size**: 16x16 pixels, 4-color gray.
  - **Design**: Simple coin (based on Kenney.nl, monochrome), with sparkle effect.
  - **Animation**: Blink (4 frames, 0.2 seconds/frame), 2-frame scale-up (0.1 seconds) on collection.

- **Effects: Stars (Background Decoration)**:
  - **Size**: 8x8 pixels, 4-color gray.
  - **Design**: Simple 4-pixel glow.
  - **Animation**: Blink (4 frames, 0.3 seconds/frame), randomly placed.

- **Tools**: Aseprite (or LibreSprite) for sprite creation; Procreate/Photoshop for rough sketches, then pixelized in Aseprite.
- **Grok Support**: Request "Grok, 8-bit-style monochrome rock 16x16 design" or "Grok, coin 16x16 blink animation code".

### 2. Background Specifications
The Mars landscape uses tiled sprites for a repeating effect, with a bonus stage overlay.

- **Mars Ground Sprite**:
  - **Size**: 256x64 pixels, 4-color gray.
  - **Design**: Rocks, craters, and a plain starry sky in a cheap 8-bit style, seamless left-to-right for tiling.
  - **Tiling**: `ParallaxComponent` scrolls right-to-left (-50 pixels/second), repeats when off-screen.
  - **Layers**: Ground (256x64) + distant sky (256x32, -25 pixels/second) for depth.

- **Bonus Stage Background**:
  - **Size**: 320x64 pixels, 4-color gray.
  - **Design**: Massive Ani-chan (blonde twin-tails, goth-loli) laying down, overlaid on Mars ground.
  - **Movement**: `ParallaxComponent` scrolls right-to-left (-100 pixels/second), ends after 10 seconds.
  - **Effects**: Monochrome stars (8x8) and coins (16x16) blink randomly.
  - **Optimization**: Reuses 256x64 ground sprite, keeps memory low (10-15KB).

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
      ], baseVelocity: Vector2(-50, 0)); // Right-to-left scroll
    }
  }

  class BonusStage extends ParallaxComponent {
    @override
    Future<void> onLoad() async {
      parallax = await gameRef.loadParallax([
        ParallaxImageData('mars_ground_mono.png', repeat: ParallaxRepeat.repeatX, velocityMultiplier: Vector2(1, 0)),
        ParallaxImageData('ani_laying_mono_gothloli.png', repeat: ParallaxRepeat.none, velocityMultiplier: Vector2(2, 0)),
      ], baseVelocity: Vector2(-100, 0)); // Faster scroll for bonus
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

3. Gameplay Specifications

- Triggers:
    - Bonus Stage: Unlocks with 1000 coins or 10 minutes of play, lasts 10 seconds.
- Movement:
    - Player: Left-right movement (-100 to 100 pixels/second), jump (32 pixels high, 0.5 seconds).
    - Obstacles: Random spawn (5-10 second intervals), speed -50 pixels/second.
    - Coins: Random spawn (3-5 second intervals), speed -50 pixels/second.
- Scoring:
    - Coin: +100 points.
    - Bonus Stage: +500 points on completion.
- Game Over: 3 collisions with rocks ends the game.

4. Monetization Specifications

- AdMob: Banner (bottom of screen), interstitial (post-game over).
- In-App Purchases (IAP): Tesla Shiba skin ($0.99), goth-loli Ani-chan skin ($1.99), King Boost ($0.99).
- Dogecoin Tipping: QR code on game-over screen for crypto donations.

5. Additional Specifications

- Sound: Pixabay 8-bit chiptune, collision sound ("piro-piro"), coin collect sound ("chin!").
- X Post Example: "8-bit-style goth-loli Ani-chan DOONs in Dogecoin Dash! !😺👑
    
    @elonmusk
    
    , is this you? [itch.io link] #GrokChallenge #DogecoinDash"

---

 🛠️ Development PlanBuilt with Flutter and Flame for a lightweight, 8-bit-style Web game. Grok assists with code, debugging, and ideas. Pro artist’s monochrome 8-bit-style goth-loli Ani-chan is the star! Live on GitHub, contributions welcome!Tech Stack

- Framework: Flutter + Flame (2D engine)
- Assets: Custom monochrome 8-bit-style Ani-chan (320x64), free 8-bit art (Kenney.nl, OpenGameArt)
- Deployment: itch.io, Game Jolt, GitHub Pages
- Monetization: AdMob (google_mobile_ads), IAP (in_app_purchase), Dogecoin tipping
- Tools: Aseprite/Procreate (for sprite art), VS Code, Filmora (10-sec trailers), Grok (AI)

Milestones

1. Prototype (1 Week):
    - 8-bit-style Shiba (16x16) running/jumping, Martian rocks (16x16), Dogecoin (16x16), Web build on GitHub Pages.
    - Pro artist refines Ani-chan (320x64, goth-loli).
    - Grok: "8-bit-style Shiba jump code" or "obstacle spawn code".
2. Alpha (2 Weeks):
    - Dogecoin King (24x24, coin sprinkle), bonus stage with Ani-chan (320x64).
    - AdMob banners/interstitials.
    - itch.io/Game Jolt launch.
3. Release (3 Weeks):
    - Skins (Tesla Shiba 16x16, Ani-chan 24x24), IAP, Dogecoin tipping.
    - 8-bit chiptune (Pixabay), 10-sec trailer (Filmora).
    - X campaign with community features.

---

 📣   Viral Strategy (#GrokChallenge)Make Dogecoin Dash a viral 8-bit-style hit on X with Grok, monochrome goth-loli Ani-chan, and Dogecoin King!

- 10-Second Trailer (Filmora): 8-bit-style Shiba (16x16), goth-loli Ani-chan (320x64, DOON!), King (24x24) sprinkling coins. Text: "Grok’s 8-bit-style Dogecoin Dash! [itch.io link] #GrokChallenge"
- Real-Time Dev: Commits like "Pro artist’s goth-loli Ani-chan DOON! added! [GitHub link] #DogecoinDash"
- Community Engagement: Polls (e.g., "Next skin? Goth-loli Cat King? SpaceX Ani? [Game Jolt link]"), Reddit posts (r/webgames, r/indiegames).
- Elon Bait: "
    
    @elonmusk
    
    , goth-loli Ani-chan’s DOON! with King? Play now! [itch.io link] #GrokChallenge"

---

 💰  Monetization

- AdMob: Banners, interstitials, est. $50-300/month at 10K plays (eCPM $0.5-3).
- IAP: Skins ($0.99-$2.99), ad removal ($1.99), King Boost ($0.99), est. $199 at 1% conversion for 10K plays.
- Dogecoin Tipping: QR code, est. $10-100 at 10K plays (0.1 DOGE tips).
- itch.io/Game Jolt: PWYW (push $1-5), AdMob, ads ($1/1,000 plays).

---

 🚀 Why Dogecoin Dash?

- Goth-loli Art Fun: Huge pro-artist goth-loli Ani-chan in 8-bit-style glory!
- Grok-Powered: AI-driven dev, live on GitHub.
- Meme Appeal: Shiba + goth-loli Ani-chan + Tesla King = X virality.
- Community-Driven: Ideas via X/GitHub.
- Fast & Free: Web play on itch.io/Game Jolt, no servers.

---

 🐾 Join the Challenge!

1. Play: Try the 8-bit-style build! itch.io (#) | Game Jolt (#)
2. Contribute: Suggest Ani-chan poses on GitHub Issues (#).
3. Share: Post scores on X with #GrokChallenge #DogecoinDash!
4. Tip: Love goth-loli Ani-chan’s DOON!? Send Dogecoin! QR Code (#)
5. Follow: Track Grok on X: [#GrokChallenge](/hashtag/GrokChallenge)

Let’s make this 8-bit-style Shiba conquer Mars with goth-loli Ani-chan’s DOON! and Dogecoin King!

@elonmusk

, are you the King? 😎

---

 📜  LicenseMIT License - Free to play, share, contribute!

---

Created with ❤️, Grok, and pro artist’s monochrome 8-bit-style goth-loli Ani-chan by [izumix77]. Powered by xAI.
