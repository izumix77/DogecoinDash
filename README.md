
# DogecoinDash 🐶💸

[![Grok Challenge](https://img.shields.io/badge/Grok-Challenge-%23GrokChallenge-blue)](https://x.com/hashtag/GrokChallenge) [![Play Now](https://img.shields.io/badge/Play-Web-brightgreen)](https://username.github.io/DogecoinDash) [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Welcome to **DogecoinDash**, an 8-bit-style, chiptune-fueled endless runner built with Flutter and Flame for the **Grok Challenge**! 🚀 Powered by Grok (xAI), this game stars a Shiba Inu dashing through Mars to grab Dogecoins, with **Dogecoin King** (Tesla-mantled, Elon-inspired) sprinkling bonus coins and **Ani-chan** (Grok’s mascot, drawn by a pro artist) as a huge monochrome 8-bit-style background, laying down with a "DOON!" in the bonus stage. Play instantly on itch.io/Game Jolt, follow live dev on GitHub, and join #GrokChallenge on X to make it viral! 😎

> **Play now**: [itch.io](#) | [Game Jolt](#) | **Follow**: [#GrokChallenge](https://x.com/hashtag/GrokChallenge) | **Contribute**: [GitHub Issues](#)

---

## 🎮 Game Concept

**DogecoinDash** is a fast, offline, 8-bit-style endless runner where a Shiba Inu sprints across Mars to collect Dogecoins. Dodge rocks and AI drones, grab bonus coins from **Dogecoin King**, and hit the bonus stage with a massive monochrome **Ani-chan** (pro artist’s 8-bit-style art) laying across the screen! Run past her to end the stage. Built with Grok’s code and a pro artist’s pixel art, live on GitHub.

- **Genre**: 2D Endless Runner
- **Platform**: Web (Flutter Web, mobile/PC via itch.io/Game Jolt)
- **Target Audience**: Indie gamers, Dogecoin fans, art fans, Elon Musk 😜
- **Tone**: Chiptune, 8-bit-style, meme-heavy with Dogecoin/Tesla vibes
- **Art Style**: 8-bit-style pixel art (monochrome, cheap, pro-artist flair)

---

## ✨ Features

- **Gameplay**:
  - Control a Shiba Inu to run, jump, slide on Mars.
  - Collect Dogecoins for score (Web Storage).
  - Dodge obstacles: Martian rocks, AI drones, meteors.
- **Dogecoin King (Elon-Inspired NPC)**:
  - Appears randomly (5% chance) with crown, sunglasses, Tesla-logo mantle.
  - Sprinkles 10 bonus Dogecoins (+100 score each) in 8-bit-style glory.
- **Ani-chan (Grok’s Mascot)**:
  - Huge monochrome 8-bit-style art (320x64 pixels) by a pro artist, laying down with a "DOON!" in bonus stage (1000 coins/10 min trigger).
  - Shiba runs past her massive sprite; stage ends when her body is cleared.
  - X appeal: "@elonmusk, Monochrome Ani-chan’s DOON! with King? 😺👑"
- **Power-Ups**:
  - **Dogecoin Magnet**: Attracts coins for 10 seconds.
  - **Tesla Boost**: 2x speed with 8-bit-style sparks! ⚡️
  - **Moon Jump**: High jumps with lunar vibes.
- **Skins**:
  - Default Shiba, Tesla Shiba, Ani-chan (IAP/unlock).
- **Monetization**:
  - **AdMob**: Banners (bottom), interstitials (post-bonus, 3-5 min).
  - **In-App Purchases**: Skins ($0.99-$2.99), ad removal ($1.99), King Boost ($0.99).
  - **Dogecoin Tipping**: QR code for crypto donations.
- **Web-First**:
  - Instant play on itch.io/Game Jolt.
  - No server, no app store, pure 8-bit-style fun.

---

## 🛠️ Development Plan

Built with **Flutter** and **Flame** for a lightweight, 8-bit-style Web game. Grok assists with code, debugging, and ideas. Pro artist’s monochrome 8-bit-style Ani-chan is the star! Live on GitHub, contributions welcome!

### Tech Stack
- **Framework**: Flutter + Flame (2D engine)
- **Assets**: Custom monochrome 8-bit-style Ani-chan (pro artist), free 8-bit art (Kenney.nl, OpenGameArt)
- **Deployment**: itch.io, Game Jolt, GitHub Pages
- **Monetization**: AdMob (`google_mobile_ads`), IAP (`in_app_purchase`), Dogecoin tipping
- **Tools**: Aseprite/Procreate (for Ani-chan art), VS Code, Filmora (10-sec trailers), Grok (AI)

### Milestones
1. **Prototype (1 Week)**:
   - 8-bit-style Shiba running/jumping, Dogecoin collection.
   - Web build on GitHub Pages.
   - Pro artist starts monochrome 8-bit-style Ani-chan (320x64).
   - Grok: "8-bit-style Shiba jump code!"
2. **Alpha (2 Weeks)**:
   - Dogecoin King (coin sprinkle), obstacles (rocks, drones).
   - Monochrome Ani-chan in bonus stage (scrolling, stage ends after her).
   - AdMob banners/interstitials.
   - itch.io/Game Jolt launch.
3. **Release (3 Weeks)**:
   - Skins (Ani-chan, Tesla Shiba), IAP, Dogecoin tipping.
   - 8-bit chiptune (Pixabay), effects (Filmora).
   - Community features via X/GitHub.

### Sample Code (Monochrome Ani-chan Bonus Stage)
```dart
import 'package:flame/components.dart';
import 'package:flame/parallax.dart';

class BonusStage extends ParallaxComponent {
  @override
  Future<void> onLoad() async {
    parallax = await gameRef.loadParallax([
      ParallaxImageData('mars_mono_8bit.png', repeat: ParallaxRepeat.repeatX),
      ParallaxImageData('ani_laying_mono.png', repeat: ParallaxRepeat.none), // 8bit風モノクロAniちゃん
    ], baseVelocity: Vector2(-100, 0)); // 右から左へ
    // モノクロキラキラコイン
    for (int i = 0; i < 5; i++) {
      add(SpriteAnimationComponent(
        animation: await gameRef.loadSpriteAnimation('coin_mono_sparkle.png', SpriteAnimationData.sequenced(amount: 4, stepTime: 0.2, textureSize: Vector2.all(16))),
        position: Vector2(50 + i * 30, 20),
      ));
    }
    // 10秒で終了
    Future.delayed(Duration(seconds: 10), () => gameRef.endBonusStage());
  }
}
````
