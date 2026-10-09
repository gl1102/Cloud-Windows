[简体中文](README.md) | [English](README.en.md) | [Русский](README.ru.md) | [日本語](README.ja.md) | [한국어](README.ko.md) | [Español](README.es.md) | [العربية](README.ar.md) | [Čeština](README.cs.md) | [Dansk](README.da.md) | [Deutsch](README.de.md) | [Esperanto](README.eo.md) | [فارسی](README.fa.md) | [Suomi](README.fi.md) | [Français](README.fr.md) | [Ελληνικά](README.gr.md) | [Magyar](README.hu.md) | [Bahasa Indonesia](README.id.md) | [Italiano](README.it.md) | [മലയാളം](README.ml.md) | [Nederlands](README.nl.md) | [Norsk](README.no.md) | [Polski](README.pl.md) | [Português](README.ptbr.md) | [Română](README.ro.md) | [Türkçe](README.tr.md) | [Українська](README.ua.md) | [Tiếng Việt](README.vn.md)

# ☁️ Cloud-Windows — 무료 클라우드 Windows 데스크톱

GitHub Actions의 무료 Windows 가상 머신을 브라우저로 접속하는 클라우드 데스크톱으로 만들어 보세요. 웹 페이지만 열면 Windows PC를 쓸 수 있고, 다 쓰면 끄면 됩니다. 완전 무료입니다.

## ✨ 기능

- 🖥️ 브라우저에서 바로 조작하는 풀 Windows 데스크톱(noVNC 웹 클라이언트)
- 📐 **자동 해상도**: 페이지 열기 후 브라우저 창 크기에 맞춰 데스크톱 해상도가 자동으로 조정됩니다. 휴대폰·PC 각각 최적화되고, 창 크기를 바꾸면 따라 조정됩니다
- 🌐 Cloudflare 터널을 통한 접속 — 공인 IP 불필요, 포트포워딩 불필요
- ⌨️ Sogou 입력기(搜狗输入法) 내장, 중국어 입력이 바로 됩니다(`Win + Space`로 중/영 전환)
- 🖱️ 휴대폰·태블릿·PC 어디서든 접속 가능
- ⏱️ 1회 최대 약 6시간 실행, 언제든 취소 가능
- 📦 **RustDesk 버전**: RustDesk가 포함된 워크플로도 있으며, 최신 RustDesk를 D 드라이브에 자동 다운로드하고 `D:\RustDesk`에 무인 설치합니다

## 🚀 사용 방법(Fork 후 바로 사용)

### 1단계: 이 프로젝트 Fork 하기

이 페이지 오른쪽 위의 **Fork** 버튼을 눌러 프로젝트를 본인 GitHub 계정으로 복사하세요. Fork이 끝나면 `사용자 이름/Cloud-Windows` 저장소로 이동합니다.

> 💡 왜 Fork해야 하나요? GitHub Actions는 본인 계정의 저장소에서만 실행할 수 있어서, Fork해야 실행 권한이 생깁니다.

### 2단계: 클라우드 데스크톱 실행

1. Fork한 저장소 페이지에서 상단 **Actions** 탭 클릭
2. 왼쪽에서 워크플로를 선택하세요(둘 중 하나):
   - **Windows Cloud Desktop**: 표준 클라우드 데스크톱
   - **Windows Cloud Desktop + RustDesk**: 표준 버전에 최신 RustDesk를 D 드라이브에 자동 다운로드하고 `D:\RustDesk`에 무인 설치(버전 하드코딩 없음, 매번 공식 최신 릴리스를 가져옴)
3. 오른쪽 **Run workflow** 버튼을 누르면 입력창 3개가 뜹니다

| 매개변수 | 설명 |
|------|------|
| VNC 비밀번호 | 데스크톱 접속 시 입력할 비밀번호. 영문+숫자 8자 이내(예: `abc12345`), **꼭 메모해 두세요** |
| 실행 시간 | 이번 클라우드 데스크톱 유지 시간(분). 기본 300(5시간), 최대 350 |
| 해상도 | 초기 데스크톱 해상도. 기본 1920x1080이며, 브라우저에서 페이지 열면 창 크기에 맞게 자동 재조정됩니다 |

4. 초록색 **Run workflow** 버튼을 눌러 확정하면 클라우드 데스크톱이 시작됩니다

### 3단계: 접속 주소 확인

1. Actions 페이지에서 방금 시작한 실행 클릭(맨 위 항목, 노란색 점은 실행 중)
2. 가상 머신이 소프트웨어를 설치하고 터널을 만들 때까지 3~5분 정도 기다리세요
3. **启动服务并建立隧道** 단계를 클릭해 로그를 펼치고 아래로 스크롤하면 이런 주소가 보입니다

```
https://xxx-xxx-xxx.trycloudflare.com/vnc.html
```

4. 이 주소를 복사해 브라우저에서 여세요(휴대폰 기본 브라우저도 OK)

### 4단계: 데스크톱 연결

1. 열린 noVNC 페이지에서 **Connect** 클릭
2. 2단계에서 설정한 VNC 비밀번호 입력
3. Windows 데스크톱이 보입니다. 사용해 보세요 🎉
4. 페이지 열기 후 약 10초 안에 데스크톱 해상도가 브라우저 창에 자동으로 맞춰집니다. 창 크기를 바꾸면 자동으로 재조정됩니다(그래픽카드가 지원하는 해상도 중에서 선택)

> ⌨️ 입력기 전환은 **Win + Space**, Sogou 병음과 영문 키보드 사이를 전환합니다.

### 5단계: 다 쓰면 종료하기

- Actions 페이지로 돌아가 해당 실행을 열고 오른쪽 위 **Cancel run** 클릭 — 가상 머신이 삭제되고 터널이 비활성화됩니다
- 설정한 실행 시간이 지나면 자동으로 종료되니 계속 돌까 봐 걱정할 필요 없습니다

## ⚠️ 주의사항

- **실행할 때마다 주소가 바뀝니다**: 이전 실행이 끝나면 예전 주소는 무효가 되니, 반드시 최신 실행 로그의 주소를 사용하세요
- **데이터는 저장되지 않습니다**: 가상 머신이 삭제되면 데스크톱의 파일·다운로드·로그인 상태가 모두 지워집니다. 중요한 파일은 미리 옮겨 두세요
- **비밀번호 규칙**: 영문+숫자만, 8자 이내. 너무 길거나 특수문자가 들어가면 접속이 안 될 수 있습니다(`Authentication failed` 표시)
- **Re-run을 누르지 마세요**: 새 데스크톱을 열려면 **Run workflow**를 누르세요. Re-run은 옛날 코드로 실행됩니다
- **느리거나 끊김**: 터널이 Cloudflare를 거치므로 중국 내 접속 속도는 네트워크 상황에 따라 다르지만, 쓸 만합니다
- **페이지가 안 열림**: 먼저 해당 실행이 아직 진행 중인지 확인하세요(노란색 점). Cancel/종료된 상태면 주소가 무효입니다

## ❓ 자주 묻는 질문

| 증상 | 원인/해결 |
|------|-----------|
| `loopback connections are not enabled` | 구버전 버그, 최신 코드로 Run workflow에서 다시 실행하세요 |
| `Server is not configured properly` | 구버전 버그, 최신 코드로 Run workflow에서 다시 실행하세요 |
| `Authentication failed` | VNC 비밀번호 오입력, 또는 비밀번호가 8자 초과/특수문자 포함 |
| 페이지에 502 / 1033 표시 | 터널이 아직 안 열렸거나 끊긴 상태 — 몇 분 기다리거나 다시 실행하세요 |
| 해상도가 자동으로 안 바뀜 | 약 10초 기다리세요. 브라우저 창이 실제로 변했는지 확인하세요. 일부 비표준 해상도는 그래픽카드 미지원이라 가장 가까운 해상도가 자동 선택됩니다 |

## 🛠️ 직접 고치고 싶다면?

워크플로 파일은 `.github/workflows/` 아래에 있습니다(`windows-vnc.yml` 표준 버전, `windows-vnc-rustdesk.yml` RustDesk 버전). GitHub 웹에서 바로 편집할 수 있고, 커밋하면 즉시 반영됩니다.
