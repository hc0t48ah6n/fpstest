# Multi-Stage Physics & 3D Benchmark

A web-browser-based, unified benchmark tool designed to evaluate the 3D graphics, physics simulation, CPU processing, and rendering performance of devices (smartphones, PCs, and tablets).

---

## English

### 🌟 Key Features

1. **One-Tap Fully Automated Measurement**
   - No complex setup required. Simply tap "Start Benchmark" to run all 7 load test stages sequentially.
2. **Uncapped Generation to Limits**
   - To prevent tests from hanging infinitely on high-performance devices, objects and particles are created without a fixed limit.
   - Each stage automatically detects when the frame rate drops to **around 10 FPS** and advances to the next test.
3. **Mobile-First UI**
   - Displays real-time FPS, active object count, and network ping in the top-left corner.
   - Features touch-friendly buttons and clear result modals tailored for mobile screens.

---

### 📊 Test Stages (7 Stages Total)

| Stage | Test Name | Workload Type | Measurement / Completion Logic |
| :--- | :--- | :--- | :--- |
| **1/7** | **3D Model Stress** | GPU / Vertex & Pixel Shaders | Spawns and rotates 3D sphere meshes in bulk. Measures until 10 FPS threshold. |
| **2/7** | **Cannon.js Rigid Physics** | CPU & GPU / Gravity & Collisions | Uses `Cannon.js` to simulate real-time gravity and rigid-body collisions. Measures until 10 FPS threshold. |
| **3/7** | **Water Surface Reflection & Splash** | CPU & GPU / Fluid & Reflection | Renders a pond with real-time environment cubemap reflections. Computes height-field wave propagation and splash particle physics on impact. Measures until 10 FPS threshold. |
| **4/7** | **Image & Texture Processing** | GPU / Memory & Texture Synthesis | Dynamically procedurally generates canvas textures applied to spawned meshes. Measures until 10 FPS threshold. |
| **5/7** | **CPU Particle Physics** | CPU / Buffer Memory & Math | Updates positions and velocities for tens/hundreds of thousands of particles in CPU memory (`TypedArray`). Measures until 10 FPS threshold. |
| **6/7** | **Auto Text Scrolling** | Browser / DOM Layout & Repaint | Generates tens of thousands of DOM characters and auto-scrolls rapidly for 10 seconds. Measures the **minimum sustained FPS**. |
| **7/7** | **CPU Bombardment & Infinite Task Queue** | CPU / Event Loop & Matrix Math | Uses `MessageChannel` to recursively queue heavy matrix/trigonometric computations before prior tasks finish. Measures until 10 FPS threshold. |

---

### 📈 Real-Time Status Panel (Top-Left)

- **FPS (Frames Per Second):**
  - `50+ FPS`: 🟢 Green (Smooth)
  - `25 - 49 FPS`: 🟡 Yellow (Moderate Load)
  - `24 FPS or lower`: 🔴 Red (Heavy Lag / Stutter)
- **OBJECTS / METRICS:** Displays current object count, particle count, computation loops, or remaining seconds.
- **PING:** Real-time round-trip latency (ms) to Google CDN servers.

---

### 🏆 Score Calculation Formula

To ensure huge metric numbers (e.g., hundreds of thousands of particles or computations) do not artificially inflate the final score, scaled weighting coefficients are applied across all stages.

$$\text{Total Score} = S_{\text{3D}} + S_{\text{Cannon}} + S_{\text{Water}} + S_{\text{Texture}} + S_{\text{CPU Particles}} + S_{\text{Text Scroll}} + S_{\text{CPU Task}}$$

#### Stage Formulas
1. **3D Models:** $\text{Count} \times 1.0$
2. **Cannon.js Rigid Physics:** $\text{Count} \times 3.0$
3. **Water Physics:** $\text{Drops} \times 2.5$
4. **Texture Processing:** $\text{Textures} \times 1.2$
5. **CPU Particles:** $\frac{\text{Particles}}{100}$
6. **Text Scroll:** $\text{Minimum FPS} \times 50$
7. **CPU Bombardment & Matrix Math:** $\text{Computations (in 10k units)} \times 1.0$

---

### 🛠 Technical Specifications

- **Renderer:** Three.js (WebGL)
- **Physics Engine:** Cannon.js
- **Styling:** Tailwind CSS, FontAwesome
- **Single-File Architecture:** Fully contained within a single `.html` file for immediate execution in any web browser.

---
---

## 日本語

### 🌟 主な特徴

1. **ワンタップ・完全自動計測**
   - 複雑な設定は一切不要。「ベンチマーク開始」をタップするだけで、全7個の負荷テストが順番に実行されます。
2. **限界値までの無制限生成**
   - ハイスペックな端末でもテストが終わらなくなるのを防ぐため、オブジェクト数やパーティクル数には固定の上限を設けていません。
   - 各ステージでフレームレートが **10 FPS 付近まで落ち込んだ段階で自動検知** し、次のテストへ移行します。
3. **スマホ最適化UI (Mobile-First UI)**
   - 画面左上に常時FPS・現在のオブジェクト数・ネットワークPingを表示。
   - 指でタップしやすいボタンデザインや結果画面を採用しています。

---

### 📊 テストステージ一覧 (全7工程)

| ステージ | テスト名 | 負荷の種類 | 計測・判定条件 |
| :--- | :--- | :--- | :--- |
| **1/7** | **3Dモデル負荷** | GPU / 頂点・ピクセルシェーダー | 3D球体メッシュを大量生成・回転。10 FPS低下まで計測。 |
| **2/7** | **Cannon.js 剛体物理** | CPU & GPU / 重力・衝突演算 | `Cannon.js` を使用し、重力と剛体衝突の物理シミュレーションを実施。10 FPS低下まで計測。 |
| **3/7** | **水面反射＆水しぶき物理** | CPU & GPU / 流体・反射 | リアルタイム環境キューブマップ反射のポンド（水面）を作成。オブジェクト着水時の波形伝播（Height-field）と水しぶき粒子の物理計算を実施。10 FPS低下まで計測。 |
| **4/7** | **画像＆テクスチャ処理** | GPU / メモリ・テクスチャ合成 | Canvasで動的にプロシージャル生成したテクスチャを貼り付けたメッシュを大量追加。10 FPS低下まで計測。 |
| **5/7** | **CPU粒子物理計算** | CPU / メモリバッファ・数値計算 | 動的にメモリ（TypedArray）を自動拡張しながら、数万〜数十万個の粒子の位置・速度更新をCPUで計算。10 FPS低下まで計測。 |
| **6/7** | **テキスト自動スクロール** | Browser / DOM再描画・レイアウト | 数万文字のDOM要素を生成し、10秒間高速オートスクロール。**10秒間の最低維持FPS** を測定。 |
| **7/7** | **CPU爆撃＆無限タスク予約** | CPU / イベントループ・行列計算 | `MessageChannel` を用い、非同期タスクが完了する前に次の重い行列・三角関数計算タスクを無限にキュー予約。10 FPS低下まで計測。 |

---

### 📈 常時ステータス表示 (画面左上)

- **FPS (Frames Per Second):**
  - `50 FPS 以上`: 🟢 緑色（快適）
  - `25 〜 49 FPS`: 🟡 黄色（やや負荷あり）
  - `24 FPS 以下`: 🔴 赤色（重度負荷・カクつき）
- **OBJECTS / METRICS:** 現在実行中のステージにおけるオブジェクト数・粒子数・計算回数・残り秒数を表示。
- **PING:** Google CDNサーバーとの通話応答速度（ミリ秒）をリアルタイム表示。

---

### 🏆 スコア算出ロジック

特定の数値（数万単位の粒子数や計算回数）だけで総合スコアが極端に膨れ上がらないよう、適切なスケーリング係数を適用して全体のバランスを整えています。

$$\text{Total Score} = S_{\text{3D}} + S_{\text{Cannon}} + S_{\text{Water}} + S_{\text{Texture}} + S_{\text{CPU Particles}} + S_{\text{Text Scroll}} + S_{\text{CPU Task}}$$

#### 各項目の計算式
1. **3Dモデル:** $\text{個数} \times 1.0$
2. **Cannon.js 剛体物理:** $\text{個数} \times 3.0$
3. **水面物理:** $\text{落下数} \times 2.5$
4. **テクスチャ処理:** $\text{枚数} \times 1.2$
5. **CPU粒子物理:** $\frac{\text{粒子数}}{100}$
6. **テキストスクロール:** $\text{最低維持FPS} \times 50$
7. **CPU爆撃＆行列計算:** $\text{計算回数(万回)} \times 1.0$

---

### 🛠 テクニカル仕様

- **レンダラー:** Three.js (WebGL)
- **物理エンジン:** Cannon.js
- **スタイル:** Tailwind CSS, FontAwesome
- **単一ファイル構成:** HTML / CSS / JavaScript を1つの `.html` ファイルに完結させているため、ブラウザで直接開くだけで即座に動作します。

---
---

## 한국어

### 🌟 주요特徴

1. **원터치 완전 자동 측정**
   - 복잡한 설정 없이 "벤치마크 시작" 버튼을 터치하기만 하면 총 7단계의 부하 테스트가 순차적으로 실행됩니다.
2. **한계치까지 무제한 생성**
   - 고성능 기기에서 테스트가 끝나지 않는 현상을 방지하기 위해 오브젝트 및 파티클 수에 고정된 상한선을 두지 않았습니다.
   - 각 단계에서 프레임 레이트가 **10 FPS 근처로 떨어지는 시점을 자동으로 감지**하여 다음 테스트로 이동합니다.
3. **모바일 최적화 UI (Mobile-First UI)**
   - 화면 좌측 상단에 실시간 FPS, 현재 오브젝트 수, 네트워크 Ping을 상시 표시합니다.
   - 모바일 환경에서 터치하기 쉬운 버튼 디자인과 결과 화면을 제공합니다.

---

### 📊 테스트 단계 목록 (총 7단계)

| 단계 | 테스트명 | 부하 유형 | 측정 및 판정 조건 |
| :--- | :--- | :--- | :--- |
| **1/7** | **3D 모델 부하** | GPU / 버텍스·픽셀 셰이더 | 3D 구체 메시를 대량 생성 및 회전. 10 FPS 저하 시점까지 측정. |
| **2/7** | **Cannon.js 강체 물리학** | CPU & GPU / 중력·충돌 연산 | `Cannon.js`를 사용하여 중력 및 강체 충돌 물리학 시뮬레이션을 수행. 10 FPS 저하 시점까지 측정. |
| **3/7** | **수면 반사 및 물보라 물리학** | CPU & GPU / 유체·반사 | 실시간 환경 큐브맵 반사가 적용된 연못(수면)을 생성. 오브젝트 착수 시 파형 전파(Height-field) 및 물보라 입자 연산 수행. 10 FPS 저하 시점까지 측정. |
| **4/7** | **이미지 및 텍스처 처리** | GPU / 메모리·텍스처 합성 | Canvas에서 동적으로 생성한 프로시저럴 텍스처를 입힌 메시를 대량 추가. 10 FPS 저하 시점까지 측정. |
| **5/7** | **CPU 입자 물리학 연산** | CPU / 메모리 버퍼·수치 연산 | CPU 메모리(`TypedArray`)를 동적으로 확장하며 수만~수십만 개 입자의 위치 및 속도 업데이트 연산 수행. 10 FPS 저하 시점까지 측정. |
| **6/7** | **텍스트 자동 스크롤** | Browser / DOM 레이아웃·재묘화 | 수만 자의 DOM 요소를 생성하고 10초간 고속 자동 스크롤 수행. **10초간의 최저 유지 FPS** 측정. |
| **7/7** | **CPU 폭격 및 무한 태스크 예약** | CPU / 이벤트 루프·행렬 연산 | `MessageChannel`을 활용하여 비동기 작업이 완료되기 전에 다음 행렬·삼각함수 연산 작업을 무한히 큐에 예약. 10 FPS 저하 시점까지 측정. |

---

### 📈 상시 상태 표시 (화면 좌측 상단)

- **FPS (Frames Per Second):**
  - `50 FPS 이상`: 🟢 초록색 (원활)
  - `25 ~ 49 FPS`: 🟡 노란색 (보통 부하)
  - `24 FPS 이하`: 🔴 빨간색 (심한 부하 / 끊김)
- **OBJECTS / METRICS:** 현재 실행 중인 단계의 오브젝트 수, 입자 수, 연산 횟수, 남은 시간을 표시.
- **PING:** Google CDN 서버와의 응답 속도(ms)를 실시간 표시.

---

### 🏆 점수 계산 로직

특정 수치(수만 단위의 입자 수나 연산 횟수)로 인해 종합 점수가 과도하게 높아지지 않도록 적절한 가중치 계수를 적용하여 균형을 맞췄습니다.

$$\text{Total Score} = S_{\text{3D}} + S_{\text{Cannon}} + S_{\text{Water}} + S_{\text{Texture}} + S_{\text{CPU Particles}} + S_{\text{Text Scroll}} + S_{\text{CPU Task}}$$

#### 항목별 계산식
1. **3D 모델:** $\text{개수} \times 1.0$
2. **Cannon.js 강체 물리학:** $\text{개수} \times 3.0$
3. **수면 물리학:** $\text{낙하 수} \times 2.5$
4. **텍스처 처리:** $\text{장수} \times 1.2$
5. **CPU 입자 물리학:** $\frac{\text{입자 수}}{100}$
6. **텍스트 스크롤:** $\text{최저 유지 FPS} \times 50$
7. **CPU 폭격 및 행렬 연산:** $\text{연산 횟수(만 회)} \times 1.0$

---

### 🛠 기술 사양

- **렌더러:** Three.js (WebGL)
- **물리 엔진:** Cannon.js
- **스타일:** Tailwind CSS, FontAwesome

- **단일 파일 구조:** HTML / CSS / JavaScript가 하나의 `.html` 파일에 구완되어 있어 웹 브라우저에서 직접 열어 즉시 실행할 수 있습니다.
