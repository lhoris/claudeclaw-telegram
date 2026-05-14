# claudeclaw-telegram

**Claude Code CLI와 Telegram을 연동하여 나만의 AI 비서를 만드는 가이드**

Claude Code를 Telegram Bot과 연결하면 텔레그램 채팅으로 Claude에게 질문하거나 명령을 내릴 수 있어요.  
DM은 물론 그룹 채팅에서도 @멘션으로 사용할 수 있습니다.

---

## 운영체제별 가이드

| OS | 상태 |
|---|---|
| ✅ Windows | 본 문서 참고 |
| 🔜 macOS | 작성 예정 |
| 🔜 Linux | 작성 예정 |

---

## 사전 준비 (Windows)

- [x] [Claude Code CLI](https://claude.ai/code) 설치 완료
- [x] [Telegram Desktop](https://desktop.telegram.org/) 설치 완료
- [ ] Telegram Bot 생성 (아래 1단계 참고)

---

## 1단계: Telegram Bot 생성

1. Telegram에서 `@BotFather` 검색 후 대화 시작
2. `/newbot` 명령어 입력

   > **BotFather 응답:**
   > ```
   > Alright, a new bot. How are we going to call it?
   > Please choose a name for your bot.
   > ```

3. Bot 표시 이름 입력 (예: `My Claude Assistant`)

   > **BotFather 응답:**
   > ```
   > Good. Now let's choose a username for your bot.
   > It must end in `bot`. Like this, for example: TetrisBot or tetris_bot.
   > ```

4. Bot username 입력 — 반드시 `bot`으로 끝나야 함 (예: `myclaudeassistant_bot`)

   > **username이 이미 사용 중인 경우:**
   > ```
   > Sorry, this username is already taken. Please try something different.
   > ```
   > 다른 username으로 다시 시도하세요.

   > **성공 시 BotFather 응답:**
   > ```
   > Done! Congratulations on your new bot. You will find it at t.me/your_bot.
   > You can now add a description, about section and profile picture for your bot,
   > see /help for a list of commands.
   >
   > Use this token to access the HTTP API:
   > 1234567890:AAxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
   >
   > Keep your token secure and store it safely,
   > it can be used by anyone to control your bot.
   > ```

5. 발급된 **Bot Token**을 복사해두기 (외부 유출 금지 ⚠️)

---

## 2단계: Claude Code에서 Telegram 플러그인 설정

Claude Code CLI 터미널에서 아래 명령어 실행:

```
/telegram:configure
```

- 1단계에서 발급받은 **Bot Token** 입력
- Access Policy(접근 정책) 선택:
  - `pairing` — 요청할 때마다 코드로 승인 (기본값)
  - `allowlist` — 미리 등록된 사용자만 접근 가능
  - `disabled` — 채널 비활성화

---

## 3단계: 봇 페어링 (DM 연동)

1. Telegram에서 내 봇에게 아무 메시지나 전송
2. 봇이 **6자리 페어링 코드** 반환
3. Claude Code 터미널에서 아래 명령어 실행:

```
/telegram:access pair <6자리코드>
```

4. 승인 완료 → 이제 Telegram DM으로 Claude와 대화 가능 🎉

---

## 4단계: 그룹 채팅 연동 (선택)

### 4-1. 봇을 그룹에 초대

Telegram 그룹 채팅방에 내 봇을 멤버로 추가합니다.

### 4-2. BotFather에서 Group Privacy 비활성화

```
@BotFather → /mybots → 봇 선택 → Bot Settings → Group Privacy → Disable
```

> ⚠️ 기본 설정(Enabled)이면 봇이 그룹 메시지를 읽지 못합니다.  
> 변경 후 봇을 그룹에서 내보냈다가 다시 초대해야 적용될 수 있습니다.

### 4-3. 그룹 ID 확인 및 등록

그룹 ID를 확인한 뒤 Claude Code 터미널에서 실행:

```
/telegram:access group add <그룹ID>
```

> 그룹 ID는 음수(`-`)로 시작하는 숫자입니다. `@userinfobot`으로 확인할 수 있어요.

### 4-4. 그룹에서 사용

그룹 채팅에서 봇을 **@멘션**하면 Claude가 응답합니다.

```
@봇이름 안녕하세요!
```

---

## 활용 예시

- 📅 일정 관리 (파일 기반 메모)
- 📈 주식/투자 정보 조회
- 💬 질문 & 답변
- 💻 코드 작성 / 리뷰 요청
- 🔍 검색 및 요약

---

## 관련 명령어 모음

| 명령어 | 설명 |
|---|---|
| `/telegram:configure` | Bot Token 설정 및 채널 초기화 |
| `/telegram:access` | 접근 현황 확인 |
| `/telegram:access pair <코드>` | 페어링 코드로 사용자 승인 |
| `/telegram:access allow <ID>` | 특정 사용자 직접 허용 |
| `/telegram:access remove <ID>` | 사용자 제거 |
| `/telegram:access group add <ID>` | 그룹 채팅 등록 |
| `/telegram:access policy <mode>` | 접근 정책 변경 |

---

## 참고 링크

- [Claude Code 공식 문서](https://claude.ai/code)
- [Telegram BotFather](https://t.me/botfather)
