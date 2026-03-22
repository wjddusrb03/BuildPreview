# BuildPreview

**See where your block will be placed before you place it.**

A lightweight Paper plugin that shows a ghost preview of the block you're about to place. Using the modern **BlockDisplay** entity (1.19.4+), it renders a smaller, glowing version of the block at the exact placement position — visible only to you.

---

## Features

- **Real-time preview** — A 70%-scale ghost block appears where you're aiming, updating every 3 ticks (~150ms)
- **Player-specific** — Only you can see your own preview. Other players won't be distracted
- **Green glow outline** — Clearly distinguishes the preview from real blocks
- **Smooth movement** — Uses teleport interpolation for fluid preview transitions
- **Replaceable block awareness** — Correctly previews on grass, ferns, dead bushes, and other replaceable blocks
- **Toggle command** — `/bp` to turn preview on/off per player
- **Zero persistence** — Preview entities are never saved to the world. Server restarts leave no ghost blocks behind
- **Automatic cleanup** — Orphaned displays are removed on server start. Previews are removed on disconnect, gamemode change, or item switch

## Requirements

| | Version |
|---|---|
| **Server** | Paper 1.21+ |
| **Java** | 17+ |
| **Dependencies** | None |

## Installation

1. Download `BuildPreview-1.0.0.jar` from the [Releases](../../releases) page
2. Place it in your server's `plugins/` folder
3. Restart the server
4. Done — hold any block and look at a surface!

## Commands

| Command | Description | Permission |
|---------|-------------|------------|
| `/bp` | Toggle preview on/off | `buildpreview.use` (default: everyone) |

**Aliases:** `/buildpreview`

## How It Works

1. Every 3 ticks, the plugin checks if you're holding a block
2. A ray trace finds the surface you're looking at (5 block range)
3. A **BlockDisplay** entity is spawned at the target position, scaled to 70% with a green glow
4. The preview updates as you look around, and disappears when you switch items or place the block
5. `Player.hideEntity()` API ensures only you can see your preview

## Technical Details

- **BlockDisplay entity** — Modern display entity, no ArmorStand hacks
- **`setPersistent(false)`** — Entities are never written to world save files
- **Scoreboard tag** (`buildpreview_ghost`) — Identifies orphaned entities for cleanup on server start
- **ConcurrentHashMap** — Thread-safe player tracking
- **Ray trace optimization** — Skips update when target block hasn't changed

## Known Limitations

- Directional blocks (stairs, slabs, logs) show their default orientation, not the actual placement direction
- Items that place as different blocks (e.g., redstone dust → redstone wire) won't show a preview
- The preview shows at 70% scale, not full size (this is intentional for visual clarity)

## Issues & Feedback

Found a bug or have a suggestion? Please open an [Issue](../../issues)!

When reporting a bug, include:
- Your server version (`/version`)
- Steps to reproduce the problem
- Any error messages from the console

---

# BuildPreview (한국어)

**블록을 설치하기 전에 미리보기를 확인하세요.**

가벼운 Paper 플러그인으로, 설치하려는 블록의 고스트 미리보기를 표시합니다. 최신 **BlockDisplay** 엔티티(1.19.4+)를 사용하여 정확한 설치 위치에 작은 발광 블록을 렌더링합니다 — 본인에게만 보입니다.

---

## 기능

- **실시간 미리보기** — 바라보는 위치에 70% 크기의 고스트 블록이 표시됩니다 (3틱, ~150ms 간격)
- **본인에게만 표시** — 다른 플레이어에게는 미리보기가 보이지 않습니다
- **초록색 발광 테두리** — 실제 블록과 명확하게 구분됩니다
- **부드러운 이동** — 텔레포트 보간을 사용하여 자연스럽게 움직입니다
- **대체 가능 블록 인식** — 잔디, 고사리, 마른 덤불 등 위에도 올바르게 미리보기가 표시됩니다
- **토글 명령어** — `/bp`로 미리보기를 켜거나 끌 수 있습니다
- **잔류 엔티티 없음** — 미리보기 엔티티는 월드에 저장되지 않습니다. 서버 재시작 시 고스트 블록이 남지 않습니다
- **자동 정리** — 서버 시작 시 고아 엔티티 자동 제거. 접속 종료, 게임모드 변경, 아이템 변경 시 미리보기 제거

## 요구 사항

| | 버전 |
|---|---|
| **서버** | Paper 1.21+ |
| **Java** | 17+ |
| **의존성** | 없음 |

## 설치 방법

1. [Releases](../../releases) 페이지에서 `BuildPreview-1.0.0.jar` 다운로드
2. 서버의 `plugins/` 폴더에 넣기
3. 서버 재시작
4. 아무 블록이나 들고 바닥을 바라보세요!

## 명령어

| 명령어 | 설명 | 권한 |
|--------|------|------|
| `/bp` | 미리보기 켜기/끄기 | `buildpreview.use` (기본: 모든 플레이어) |

**별칭:** `/buildpreview`

## 작동 원리

1. 3틱마다 플레이어가 블록을 들고 있는지 확인
2. 레이 트레이스로 바라보는 표면 탐지 (5블록 범위)
3. 해당 위치에 70% 크기, 초록색 발광의 **BlockDisplay** 엔티티 생성
4. 시선 이동에 따라 미리보기 업데이트, 아이템 변경이나 블록 설치 시 사라짐
5. `Player.hideEntity()` API로 본인에게만 표시

## 알려진 제한 사항

- 방향이 있는 블록(계단, 반블록, 원목)은 기본 방향으로 표시됩니다 (실제 설치 방향과 다를 수 있음)
- 아이템과 블록이 다른 경우(예: 레드스톤 가루 → 레드스톤 와이어) 미리보기가 표시되지 않습니다
- 미리보기는 70% 크기로 표시됩니다 (시각적 구분을 위한 의도된 디자인)

## 문제 및 피드백

버그를 발견하거나 제안이 있으신가요? [Issue](../../issues)를 열어주세요!

버그 리포트 시 포함해 주세요:
- 서버 버전 (`/version`)
- 문제 재현 방법
- 콘솔 에러 메시지 (있다면)

---

## License

This project is provided as-is. The compiled JAR is freely available for use on any Minecraft server.
