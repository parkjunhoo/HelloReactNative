<img src="https://blog.kakaocdn.net/dn/UZlxo/btsOwMzDv9v/AHK9znBkZAOcPAwYhH3Ab1/img.gif">



# React Native 개발환경 설정 가이드

> 리액트 네이티브 공식 페이지를 따름 (2025-06-12 기준)
> 
> 참고: [Get Started with React Native](https://reactnative.dev/docs/environment-setup)

React Native allows developers who know React to create native apps. At the same time, native developers can use React Native to gain parity between native platforms by writing common features once.

## 대상 플랫폼
- **Windows & Android**

---

## 1. Chocolatey 설치

### 1.1 설치 페이지
[Chocolatey 설치 페이지](https://chocolatey.org/install)

> Chocolatey is software management automation for Windows that wraps installers, executables, zips, and scripts into compiled packages. Chocolatey integrates w/SCCM, Puppet, Chef, etc. Chocolatey is trusted by businesses to manage software deployments.

### 1.2 Chocolatey 설치 과정

#### 1단계: PowerShell 실행
- PowerShell을 **관리자 권한으로 실행**

#### 2단계: 실행 정책 확인
```powershell
Get-ExecutionPolicy
```

**결과에 따른 조치:**
- `AllSigned` → 다음 단계로 진행
- `Restricted` → 아래 명령어 실행 (보안 정책 해제)
  ```powershell
  Set-ExecutionPolicy AllSigned
  ```
  - A (모두 예) 선택

#### 3단계: Chocolatey 설치 명령어 실행
```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

---

## 2. Chocolatey로 Node.js, JDK 설치

### 2.1 설치 과정
1. **CMD를 관리자 권한으로 실행**
2. 다음 명령어 입력:
   ```cmd
   choco install -y nodejs-lts microsoft-openjdk17
   ```

### 2.2 버전 요구사항
- **Node.js**: 버전 18 이상
- **JDK**: 17 권장
- *React Native 공식문서 기준*

---

## 3. Android Studio 설치 및 셋팅

### 3.1 Android Studio 다운로드
[Android Studio 다운로드](https://developer.android.com/studio?hl=ko)

> Android Studio provides app builders with an integrated development environment (IDE) optimized for Android apps.

### 3.2 SDK 설정

#### 3.2.1 SDK Manager 접근
1. 안드로이드 스튜디오 실행
2. 프로젝트 선택 화면에서 **케밥 메뉴( ⋮ )**에서 **SDK Manager** 실행

#### 3.2.2 SDK Platforms 설정
1. `Languages & Frameworks` → `Android SDK` → `SDK Platforms`
2. 하단 **Show Package Details** 체크
3. **Android 15.0 (바닐라크림) SDK** 선택 (React Native 공식문서 권장)

**설치할 항목들:**
- Android SDK Platform 35
- Intel X86_64 Atom System Image
- Google APIs ARM 64 v8a System Image
- Google APIs Intel x86_64 Atom System Image
- Google Play ARM 64 v8a System Image
- Google Play Intel x86_64 Atom System Image

4. **Apply**를 눌러 설치 진행

#### 3.2.3 SDK Tools 설정
1. `Languages & Frameworks` → `Android SDK` → `SDK Tools`
2. **Android SDK Build-Tools 36** 선택
3. **35.0.0** 체크
4. **Apply** → **OK**

### 3.3 Virtual Device 설정
1. 케밥메뉴 → **Virtual Device Manager** → **Add (+)**
2. 기종 선택 → **API 35** 선택

> **참고**: Virtual Device를 에뮬레이팅 하기 위해서는 BIOS에서 활성화 필요
> - **Intel**: VT-x
> - **AMD**: SVM
> 
> (제조사별 바이오스 설정은 인터넷 검색 필요)

---

## 4. 환경 변수 설정

### 4.1 ANDROID_HOME 설정
1. 환경 변수 → 사용자 변수 → **새로만들기**
   - **변수 이름**: `ANDROID_HOME`
   - **변수 값**: `%LOCALAPPDATA%\Android\Sdk`

### 4.2 PATH 추가
1. 사용자 변수 → **편집** → **새로만들기**
2. 다음 경로 추가:
   ```
   %LOCALAPPDATA%\Android\Sdk\platform-tools
   ```
3. **확인**

---

## 5. React Native CLI 실행

### 5.1 프로젝트 생성
1. **터미널** → cd로 경로 지정 
   - ⚠️ **주의**: 경로에 한글이 있으면 안됨
2. 다음 명령어 실행:
   ```bash
   npx @react-native-community/cli@latest init 프로젝트이름
   ```
3. `y` 선택

### 5.2 실행 명령어
- **Android**: 
  ```bash
  npx react-native run-android
  ```
- **iOS**: 
  ```bash
  npx react-native run-ios
  ```

---
